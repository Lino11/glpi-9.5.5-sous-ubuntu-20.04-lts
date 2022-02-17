# glpi-9.5.5-sous-ubuntu-20.04-lts
mise à jour
# apt-get update
# apt-get upgrade -y
Installation LAMP(mariadb, apache2,php)
# apt install mariadb-server apache2 libapache2-mod-fcgid php7.4-fpm
# apt install php7.4-mysql php7.4-mbstring php7.4-gd php7.4-xml php7.4-intl php7.4-ldap php-apcu php7.4-xmlrpc php7.4-zip php7.4-bz2 php7.4-imap php-cas
Télécharger le glpi dans /var/www
# cd /var/www
# wget https://github.com/glpi-project/glpi/releases/download/9.5.7/glpi-9.5.7.tgz
# tar zxvf glpi-9.5.7.tgz
Création de la base de données avec le mdp root
# mysql -u root -p
>create database glpi;
>create user glpi@localhost;
>set password for glpi@localhost=PASSWORD('glpi');
>grant all privileges on glpi.* TO glpi@localhost;
>quit
Creer un fichier glpi.conf dans /etc/apache2/conf-available/
# nano /etc/apache2/conf-available/glpi.conf
copier ce contenue dedans:
Alias /glpi /var/www/glpi

<Directory /var/www/glpi>
  Options None
  AllowOverride Limit Options FileInfo
  <IfModule mod_authz_core.c>
    Require all granted
  </IfModule>
  <IfModule !mod_authz_core.c>
    Order deny,allow
    Allow from all
  </IfModule>
</Directory>
<Directory /var/www/glpi/install>
  <IfModule mod_authz_core.c>
  # Apache 2.4
    Require all granted
  </IfModule>
  <IfModule mod_php7.c>
    php_value max_execution_time 0
    php_value memory_limit -1
  </IfModule>
</Directory>
<Directory /var/www/glpi/config>
  Order Allow,Deny
  Deny from all
</Directory>
<Directory /var/www/glpi/locales>
  Order Allow,Deny
  Deny from all
</Directory>
<Directory /var/www/glpi/install/mysql>
  Order Allow,Deny
  Deny from all
</Directory>
<Directory /var/www/glpi/scripts>
  Order Allow,Deny
  Deny from all
</Directory>

Activer modules et fichiers de config
# a2enmod proxy_fcgi fcgid alias 
# a2enconf php7.4-fpm glpi 
redemarrer les services
# systemctl restart php7.4-fpm apache2




