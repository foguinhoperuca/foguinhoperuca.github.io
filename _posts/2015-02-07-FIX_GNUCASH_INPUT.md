---
layout: post
title: Erro no Input GNUCASH
---

Fica como lembrete: ao instalar o GNUCASH +2.6.3 no Ubuntu 14.10, a entrada de dados pelo teclado fica comprometida (o que é digitado não aparece na app). Para consertar isso é necessário instalar o pacote "ibus-gtk":

<pre>
jefferson@nami:~$ sudo apt-get install ibus-gtk
</pre>

E depois basta rodar o comando:

<pre>
jefferson@nami:~$ ibus exit
</pre>

Pronto! Problema resolvido!

## Fontes:

* <a href="https://twitter.com/_sgeorgi/status/534367616568426496">Dica do Sebastian Georgi (Twitter)</a>
* <a href="https://bugs.launchpad.net/ubuntu/+source/gnucash/+bug/1306500">Bug reportado no Launchpad (#1306500)</a>
