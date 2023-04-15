1. Install Alpine On virtual machine
2. next step :

Installing prerequisites for rAthena :

login root

apk update

apk upgrade

apk add build-base pcre pcre-doc pcre-dev mingw-w64-gcc zlib-dev git make cmake libstdc++ gcc g++ libuv-dev openssl-dev hwloc-dev automake libtool autoconf linux-headers clang clang-dev

Installing prerequisites for php :

apk add php8-common php8-session php8-iconv php8-json php8-gd php8-curl php8-xml php8-mysqli php8-imap php8-cgi fcgi php8-pdo php8-pdo_mysql php8-soap php8-xmlrpc php8-posix php8-mcrypt php8-gettext php8-ldap php8-ctype php8-dom php8-simplexml

if phpmyadmin error missing session

or check php info new version 

apk add php81 php81-mbstring php81-common php81-session php81-iconv php81-json php81-gd php81-curl php81-xml php81-mysqli php81-imap php81-cgi fcgi php81-pdo php81-pdo_mysql php81-soap php81-xmlrpc php81-posix php81-mcrypt php81-gettext php81-ldap php81-ctype php81-dom pDhp81-simplexml


Install Apache2

apk add apache2 php$phpverx-apache2

test in browser localhost /127.0.0.1/ip

Install MariaDB server and development libraries

apk add mysql mysql-client mariadb-dev

or

apk add mariadb mariadb-common mariadb-client mariadb-dev

/etc/init.d/mariadb setup

mysql_secure_installation

(optional) we can create in phpmyadmin GUI

for test:

CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';

GBRANT ALL PRIVILEGES ON * . * TO 'user'@'localhost';

FLUSH PRIVILEGES;

Install phpmyadmin

mkdir -p /usr/share/webapps/

cd /usr/share/webapps

wget http://files.directadmin.com/services/all/phpMyAdmin/phpMyAdmin-5.0.2-all-languages.tar.gz

if error connections

we cant download :

https://www.phpmyadmin.net/downloads/

copy link download last version

download using wget

wget https://files.phpmyadmin.net/phpMyAdmin/5.2.1/phpMyAdmin-5.2.1-all-languages.tar.gz

tar zxvf phpMyAdmin-5.0.2-all-languages.tar.gz

rm phpMyAdmin-5.0.2-all-languages.tar.gz 

mv phpMyAdmin-5.0.2-all-languages phpmyadmin

chmod -R 777 /usr/share/webapps/

ln -s /usr/share/webapps/phpmyadmin/ /var/www/phpmyadmin

or

ln -s /usr/share/webapps/phpmyadmin/ /var/www/localhost/htdocs/phpmyadmin

test run in browser : http://your-ip/phpmyadmin

Clone rAthena repository

git clone https://github.com/rathena/rathena.git

Run the configure script

You can change the option

enable-prere to yes if you want pre-renewal mode

enable-vip if you want to enable the VIP feature

enable-packetver to any client version you want to use.

example :

./configure --enable-epoll=yes --enable-prere=no --enable-vip=no --enable-packetver=20180620

Finally compile rAthena

login user no root alpine

cd rathena

configure char,iner, and map for basicly

./configure --enable-epoll=yes --enable-prere=no --enable-vip=no --enable-packetver=20180620

make clean && make server

Configure the database (optional) and we can create and import databases on phpmyadmin!!!

login root on alpine

mysql -u root -p

CREATE USER 'alpinero'@'localhost' IDENTIFIED BY 'changeme';

CREATE DATABASE alpinero;

GRANT ALL ON alpinero.* TO 'alpinero'@'localhost';

FLUSH PRIVILEGES;

quit;

cat ./sql-files/*.sql | mysql -u alpinero -p alpinero

DONE!

source :

https://github.com/rathena/rathena/wiki/Install-on-Ubuntu
