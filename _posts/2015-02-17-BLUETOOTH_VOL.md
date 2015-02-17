---
layout: post
title: Nokia E63 Bluetooth no GNU/Linux Ubuntu
---

Introdução:
Este artigo ensina a conectar o o seu celular (Nokia E63) ao linux (Ubuntu 10.04) e compartilhar a conexão da internet do seu celular com o seu PC (como uma conexão de emergência ou ainda se você tiver um plano generoso de dados, o que hoje em dia já não é mais uma raridade ^^”) além de mostrar mais algumas funcionalidades básica. Nível: iniciante.

# Sobre o Bluetooth:

**Bluetooth** é uma especificação industrial para áreas de redes pessoais sem fio (Wireless personal area networks - PANs). O Bluetooth provê uma maneira de conectar e trocar informações entre dispositivos como telefones celulares, notebooks, computadores, impressoras, câmeras digitais e consoles de videogames digitais através de uma frequência de rádio de curto alcance globalmente não licenciada e segura. As especificações do Bluetooth foram desenvolvidas e licenciadas pelo (em inglês) Bluetooth Special Interest Group.
**Fonte:** wikipedia.

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//usb-bluetooth-dongle.jpg)

Adaptador bluetooth vendido em qualquer loja. Em SP, na vila Olímpia você acha por uns R$25,00 ou ainda no [Deal Extreme](“http://www.dealextreme.com/”) por uns US$1.80 (R$3,60 aproximadamente).

## Pondo a mão na massa.

No linux o suporte ao bluetooth é bem tranquilo. O Ubuntu (versão 10.04, enquanto escrevo) já vem com o gerenciador de conexões bluetooth (gnome-bluetooth). Quando um dispositivo é conectado, o símbolo característico ![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//BlueTooth.png) irá aparecer ao lado do relógio.

Como dica, o blueman também irá mostrar o ícone padrão do bluetooth perto do relógio. Basta clickar com o botão direito em cima do ícone para descobrir qual é o correto (no meu caso normalmente é o ícone mais a esquerda). Também pode ser acessado pelo menu Sistema ==> Preferência ==> Bluetooth manager.

Caso ainda não tenha instalado o suporte ao bluetooth no sistema digite no terminal. Aproveitando também instalar o ppp para suporte à conexões discadas e o obexftp para transferir arquivos entreo o PC e o celular.
No Ubuntu, como root:
$ sudo apt-get install bluez-utils bluez-pin ppp blueman obexftp bluetooth

Para verificar se o sistema reconheceu corretamente o seu dispositivo basta dar os seguintes comandos:

### lsusb.

lista todos os dispositivos usb conectados ao seu PC.

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//lsusb.png)

No meu caso, a primeira linha (_Bus 002 Device 008: ID 0a12:0001 Cambridge Silicon Radio, Ltd Bluetooth Dongle (HCI mode)_) contém as informações do bluetooth conectado ao meu PC.

### hcitool scan.

Este comando vai procurar dispositivos com bluetooth ativado e marcados com “descobrível”. Esta é uma boa hora para ligar o suporte ao bluetooth no seu celular. ;). Também copie o mac address para utilizar posteriomente, em caso de problemas.

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//hcitool_scan.png)

### hciconfig.

Programa para configurar dispositivos bluetooth. A opção -a imprime na tela o conjunto mais completo de informações.

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//hciconfig.png)

## Pairing.

Este processo consiste em fazer o seu PC identificar o seu celular para poder trocar informações com ele. Iremos utilizaro o blueman para isso.
Escolha a opção “setup novo dispositivo”. Basta seguir o bom e velho esquema “Next, Next and Finish”.

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//add_device01.png)

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//add_device02.png)

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//add_device03.png)

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//add_device04.png)

## Enviando/Recebendo arquivos.

## Conexão GPRS.

Para tornar o seu celular um modem basta utilizar o ppp. No meu caso eu vou me conectar através de um celular com chip da claro (SP). Vamos configurar o blueman para fazer esse serviço .

### Informações:

	<li>**_*99#**_

	<li>utilizar a **_vpn claro.com.br**_.

Para conectar, escolha a opção Serial Port (Porta Serial) e click em forward (próximo). Se der certo, uma mensagem de sucesso será mostrada.

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//conexao_GPRS.png)

## Verificando o Consumo.

Ainda assim com os planos 3G mais generosos, é interessante ficar atento a quantidade da franquia consumida. Para isso clickar com o botão direito no ícone do blueman e escolher a opção Network Usage.

![Alt text](../../../images/posts/2015-02-17-BLUETOOTH_VOL//network_usage.png)

## Conclusão.

Como foi apresentado, o uso do bluetooth no linux não tem mistério. Os utilitários são simples e diretos e resolvem a maioria dos problemas pela interface visual, o que ajuda um novato, que ainda não tem muita intimidade com a linha de comando.
O compartilhamento da internet é fácil de fazer mas tem um pequeno truquezinho, o qual eu apanhei no começo, que é colocar o número correto da discagem para Claro (SP) e a vpn dela. Mais interessante que eu achei essa informação “sem-querer” através do network manager, adicionando uma conexão mobile dele. Os valores apresentados no artigo são os default para conexão com a Claro no network manager.

## Referências:

Além da minha experência na instalação e configuração foram consultado alguns sites:

(colocar como links, por favor =) ):
https://help.ubuntu.com/community/BluetoothDialup
https://help.ubuntu.com/community/BluetoothSetup
http://ubuntuforums.org/showthread.php?t=111455
https://wiki.ubuntu.com/HardwareSupportComponentsBluetoothUsbAdapters
http://pt.wikipedia.org/wiki/Bluetooth
http://www.dealextreme.com/

That's all folks!
