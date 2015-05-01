---
layout: post
title: Configuração Driver Sis 771/671 no Ubuntu.
---

# O Problema.

A placa de vídeo Sis 771/671 é conhecida por dar muita dor de cabeça para configurar, geralmente sendo usado o driver vesa com resolução de 480x600como fallback (o que é obviamente péssimo).

O notebook testado foi o _**Positivo Premium modelo SIM**_ com processador X86_64, apelidado carinhosamente por mim de [Yukina](http://yuyuhakusho.wikia.com/wiki/Yukina "Yukina - Yu Yu Hakusho"). A distribuição é o Ubuntu 14.10. Durante a instalação da distro não tive nenhum problema com resolução. O problema foi ocorrer logo após a instalação, no primeiro uso.

## Como Identificar a sua Placa de Vídeo.

Para verificar a se a sua placa de vídeo é realmente a famigerada Sis 771/671 faça o seguinte:

<pre>
jefferson@yukina:~$ lspci | grep VGA
01:00.0 VGA compatible controller: Silicon Integrated Systems [SiS] 771/671 PCIE VGA Display Adapter (rev 10)
</pre>

Se você encontrou a linha **01:00.0 VGA compatible controller: Silicon Integrated Systems [SiS] 771/671 PCIE VGA Display Adapter (rev 10)** então bingo! Continue lendo para você saber como resolver o problema.

# Driver Nativo

A boa notícia é que existe um driver nativo para esta placa. O mesmo pode [ser encontrado no github](https://github.com/hellnest/xf86-video-sismedia-0.9.1 "Repositório do driver.").

## Alternativa 00: Driver Empacotado.

Na minha experiência não encontrei nenhum pacote com o driver já pré-compilado e pré-configurado, o que eu achei particularmente estranho. Afinal, o Ubuntu e o Debian, sendo distribuições user-friendly, deveriam ter uma solução pronta para um problema relativamente comum.

Durante a pesquisa vi a sugestão para instalar o pacote _**xserver-xorg-video-sis**_ para resolução do problema. Entretanto, esse pacote não está no repositório do Ubuntu 14.10. Em seu lugar encontrei o pacote _**xserver-xorg-video-sisusb**_ (note o **usb** a mais no final), que em teoria deveria fazer o mesmo serviço. Obviamente, ele não o fez, pois o mesmo já encontrava-se instalado.

## Alternativa 01: Compilando o Driver.

A alternativa mais direta seria compilar o driver e instalá-lo como nos bons e velhos tempos.

Entretanto, vale salientar que a minha experiência não obteve êxito. A compilação falhou devido a falta da biblioteca **xaa.h**, a qual não consegui encontrá-la (_**aparentemente**_ ela está ligada a uma versão antiga da biblioteca **xorg-dev** e foi removida do upstream - Debian - justamente por não estar sendo atualizada e nem recebendo nenhum tipo de manutenção).

Portanto, não posso atestar que os passos mostrados a seguir serão sufficientes para instalação, apesar de parecerem simples e óbvios, cumprindo com o seu objetivo.

### Obtendo as Dependências.

<pre>
jefferson@yukina:~$ sudo apt-get install git xorg-dev mesa-common-dev libdrm-dev libtool build-essential
</pre>

### Obtendo o Código Fonte do Driver.

<pre>
jefferson@yukina:~$ git clone git://github.com/hellnest/xf86-video-sismedia-0.9.1.git
</pre>

### Pré-Configurando a Compilação do Driver.

Note que é necessário adicionar o parâmetro de configuração:

**--prefix=/usr --disable-static**
<pre>
jefferson@yukina:~$ cd xf86-video-sismedia-0.9.1
</pre>

<pre>
jefferson@yukina:~/xf86-video-sismedia-0.9.1$ ./configure --prefix=/usr --disable-static
</pre>

### Compilando o Driver.

Comando de compilação tradicional:
<pre>
jefferson@yukina:~$ make
</pre>

### Instalando o Driver.

Comando de instalação tradicional:
<pre>
jefferson@yukina:~$ sudo make install
</pre>

### Configurando o Xorg.

A dica original sugere que o arquivo de configuração abaixo que não funcionou na minha experiência.

<pre>
Section "Device"
Identifier "Configured Video Device"
Option "UseTiming1280" "yes"
EndSection

Section "Monitor"
Identifier "Configured Monitor"
EndSection

Section "Screen"
Identifier "Default Screen"
Monitor "Configured Monitor"
Device "Configured Video Device"
EndSection
</pre>

Sugiro que seja utilizado o arquivo com as seguintes configurações:

<pre>
Section "Device"
 Identifier  	"Device0"
 Driver      	"sisfb"
 VendorName  	"Silicon Integrated Systems [SiS]"
 BoardName   	"771/671 PCIE VGA Display Adapter"
 BusID		"PCI:1:0:0"
 Option 	"UseTiming1280" "yes"
 Option 	"EnableSiSCtrl" "no"
 Option 	"DRI" "off"
 Option 	"MergedFB" "auto"
 Option 	"MetaModes" "1280x1024-1280x800"
 Option 	"MergedDPI" "100 100"
EndSection

Section "Monitor"
Identifier "External LSD"
EndSection

Section "Monitor"
Identifier "Laptop Screen"
EndSection

Section "Screen"
       Identifier "Screen0"
       Device     "Videocard0"
       Monitor    "Main monitor"
       DefaultDepth     24
       SubSection "Display"
               Viewport   0 0
               Depth     16
               Modes    "800x600" "640x480"
       EndSubSection
       SubSection "Display"
               Viewport   0 0
               Depth     24
               Modes    "1280x800" "1024x768" "800x600" "640x480"
       EndSubSection
       EndSection

Section "Screen"
       Identifier "Screen1"
       Device     "Videocard1"
       Monitor    "Second Monitor"
       DefaultDepth     24
       SubSection "Display"
               Viewport   0 0
               Depth     24
               Modes    "1280x800" "1024x768" "800x600" "640x480"
       EndSubSection
       EndSection

Section "ServerFlags"
  Option "Xinerama" "true"
 
EndSection

Section "ServerLayout"
       Identifier     "Multihead layout"
       Screen         0 "Screen0"
       Screen         1 "Screen1" LeftOf "Screen0"
       EndSection
</pre>

Para tanto basta copiar a configuração acima no arquivo _**/etc/X11/xorg.conf**_
<pre>
jefferson@yukina:~$ sudo vim /etc/X11/xorg.conf
</pre>

**Nota**: No vim basta aperta **i** para inserir; **SHIFT + INSERT** para colar o texto (que já está salvo no buffer - vulgo clipboard); **:wq** para salvar e sair.

Para que a configuração tenha efeito, é necessário reiniciar o computador.

## Alternativa 02: Utilizando um Driver Pré-Compilado.

No meu caso eu me deparei com o seguinte site [Easy Linux tips project - SiS 671 or 771 video card in Linux Mint 13, Xubuntu 12.04 and Lubuntu 12.04 ](https://sites.google.com/site/easylinuxtipsproject/sis "Página com a solução." ). Nele, existe um [arquivo compactado](https://sites.google.com/site/easylinuxtipsproject/file-closet/sis-64-bit-1204.tar.gz?attredirects=0 "Driver para X86_64") que possui o driver pré-compilado para X86_64, juntamente com um arquivo de configuração do xorg. Existe uma versão do [driver para i386](https://sites.google.com/site/easylinuxtipsproject/file-closet/sis-32-bit-1204.tar.gz?attredirects=0 "Driver para i386") também.

### Instalando o Driver.

A instalação é feita copiando os arquivos _**sis671_drv.***_ para _**usr/lib/xorg/modules/drivers**_.
<pre>
jefferson@yukina:~$ tar xvfz sis-64-bit-1204.tar.gz
</pre>

<pre>
jefferson@yukina:~$ cd sis-64-bit-1204
</pre>

<pre>
jefferson@yukina:~/sis-64-bit-1204$ sudo mv sis671_drv.* /usr/lib/xorg/modules/drivers
</pre>

### Configurando o Xorg.

Os driver funcionam perfeitamente, resolvendo o problema mas o arquivo de configuração indicado no site não está adequado. Foi necessário utilizar a segunda versão do arquivo citada na **alternativa 01** para resolver o problema.

<pre>
jefferson@yukina:~/sis-64-bit-1204$ sudo vim /etc/X11/xorg.conf
</pre>

**Nota**: No vim basta aperta **i** para inserir; **SHIFT + INSERT** para colar o texto (que já está salvo no buffer - vulgo clipboard); **:wq** para salvar e sair.

# Conclusão

A placa Sis 671/771 é realmente complicada, tendo um suporte aquém do esperado no Ubuntu. Mas mesmo assim é possível resolver o problema com um pouco de paciência e alguas poucas gambiarras.

Como visto acima, para resolver o problema com a placa Sis 671/771 no Ubuntu a melhor solução encontrada foi baixar o driver pré-compilado e adicionar a configuração correta no arquivo _**/etc/X11/xorg.conf**_.

As outras opções como tentar instalar o driver de um pacote do repositório oficial ou mesmo compilá-lo manualmente falharam.

Fica para o futuro a opção de empacotar o driver para facilitar a instalação de outras pessoas.

# Bibliografia Consultada:

* <a href="https://sites.google.com/site/easylinuxtipsproject/sis">Easy Linux Tips Project</a>
* <a href="http://ubuntuforums.org/showthread.php?t=958967&page=84">Ubuntu Forums</a>
* <a href="http://www.vivaolinux.com.br/dica/Configurando-SIS-67172-no-Ubuntu-1404">Dica do usuário morvan bliasby no Viva o Linux</a>
* <a href="http://www.fredericomarinho.com/instalar-o-driver-da-placa-de-video-sis-671771-no-linux-mint-11/#axzz31HlXPXmz">Site do Frederico Marinho</a>
* <a href="http://ubuntuforum-br.org/index.php/topic,112445.0.html">Ubuntu Forum - BR</a>

# Licença.

Este artigo pode ser encontrado no endereço [http://jeffersoncampos.eti.br/2015/04/14/Fix_ubuntu_driver_sis_771_671.html](http://jeffersoncampos.eti.br/2015/04/14/Fix_ubuntu_driver_sis_771_671.html "Site do Autor Jefferson Campos") licenciado pela GNU FDL.
