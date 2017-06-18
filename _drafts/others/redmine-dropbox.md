# Using Dropbox as Remote Storage (Bonus: Installing Redmine).

Short description here.

# Use Case: Redmine.

## Get The Source Code!

## Configure Database

### Mysql

* Prepare Dropbox
* Symbolic Link
* User's permission
* Fix Apparmor
* Show the pitfall and why it doesn't work

### Using Sqlite

Para usar o sqlite com o redmine, não há segredo: basta configurar o arquivo <app_root>/confg/database.yml, conforme o especificado abaixo:

jefferson@nami:~/universal/projects/redmine$ vim config/database.yml

Note que não é necessário configurar os ambientes development e tests. Como, provavelmente, você não estará desenvolvendo a ferramenta, apenas utilizrá o redmine, esses ambientes tornam-se desnecessários.

## Install Libraries

### Bundle

### Others

## Run Server

# Conclusion.
