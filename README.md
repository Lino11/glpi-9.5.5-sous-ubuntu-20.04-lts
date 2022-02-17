# glpi-9.5.5-sous-ubuntu-20.04-lts
mise à jour
# apt-get update
# apt-get upgrade -y
Installation LAMP(mariadb, apache2,php)
# apt install mariadb-server apache2 libapache2-mod-fcgid php7.4-fpm
# apt install php7.4-mysql php7.4-mbstring php7.4-gd php7.4-xml php7.4-intl php7.4-ldap php-apcu php7.4-xmlrpc php7.4-zip php7.4-bz2 php7.4-imap php-cas
Télécharger le glpi dans /var/www
# cd /var/www
# wget https://github.com/glpi-project/glpi/releases/download/9.5.5/glpi-9.5.5.tgz
# tar zxvf glpi-9.5.5.tgz 

