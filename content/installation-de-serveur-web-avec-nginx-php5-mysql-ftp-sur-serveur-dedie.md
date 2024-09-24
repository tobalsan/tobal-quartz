---
title: "Installation de Serveur Web avec NGINX, PHP5, MySQL, FTP sur Serveur Dédié"
date: "2016-03-08"
tags:
  - "code"
coverImage: "serveur-web-debian.jpg"
---

Voici un petit manuel "tout en un" pour servir de mémo. J'effectue ces opérations pour un **serveur dédié sous Debian Wheezy 64bits**, mais il ne devrait y avoir aucun souci si vous suivez ces manipulations sous Debian Squeeze.<!--more-->

Pour le serveur web, nous allons ici installer:

- **NGINX**: Je préfère [NGINX](http://wiki.nginx.org/Main) à Apache car il est plus rapide (même si la dernière version d'apache se rapproche) et moins gourmand en ressources
- **PHP5**: On utilisara PHP5 avec [PHP-FPM](http://php-fpm.org/). PHP-FPM fonctionne particulièrement bien avec NGINX et permet également d'optimiser les ressources serveur
- **MySQL version 5.5**
- **[PureFTPD Mysql](http://www.pureftpd.org/project/pure-ftpd)**: PureFTPD est un très bon serveur FTP qui remplit son rôle à la perfection. La version estampée MySQL permet de gérer le utilisateur via une base MySQL (et donc directement avec [phpmyadmin](http://www.phpmyadmin.net/home_page/index.php)).

Pour commencer, placez vous en utilisateur **root**:

```
$ sudo su
```

Si il vous dit

```
-bash: sudo: command not found
```

vous devez installer sudo:

```
$ apt-get install sudo
```

Sinon vous pouvez vous logger directement en tant que root.

## [](#installation-mysql)Installation de MySQL

On commence par installer **MySQL**, c'est le plus rapide.

```
$ apt-get install mysql-server mysql-client
```

Le systême va vous demander de créer un mot de passe pour l'utiliateur root. Notez-le bien, on va s'en resservir dans pas longtemps (et de toute façon c'est bien de noter ses mots de passe sinon on les oublie).

## [](#installation-nginx)Installation de NGINX

Par défaut sous Debian Wheezy, si vous installez NGINX directement vous vous retrouverez avec la version 1.2.x, qui est loin d'être la plus récente. Pour obtenir la dernière version stable, vous devez ajouter les sources du dépot [DotDeb](http://www.dotdeb.org/):

```
$ vim /etc/apt/sources.list
```

Et ajoutez y les deux lignes suivantes:

```
deb http://packages.dotdeb.org wheezy all
deb-src http://packages.dotdeb.org wheezy all
```

Si vous êtes sur Debian Squeeze remplacez "wheezy" par "squeeze". Ensuite, vous devrez obligatoirement récupérer la clé pour accéder au dépôt DotDeb:

```
$ wget http://www.dotdeb.org/dotdeb.gpg
$ cat dotdeb.gpg | sudo apt-key add -
```

Ensuite vous pouvez installer NGINX:

```
$ apt-get update
$ apt-get install nginx
```

Vous devriez normalement avoir la version 1.4 de NGINX. Démarrez NGINX de suite:

```
$ service nginx start
```

Si vous avez tout bien installé, en vous rendant à l'adresse IP de votre serveur, via votre navigateur, vous devriez voir s'afficher l'écran suivant:

[![Écran d'accueil NGINX](https://github-camo.global.ssl.fastly.net/5c3a514085975d5ef344c1160c24385ea235b676/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f6e67696e782e706e67)](https://github-camo.global.ssl.fastly.net/5c3a514085975d5ef344c1160c24385ea235b676/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f6e67696e782e706e67)

## [](#installation-de-php5)Installation de PHP5

Pour installer PHP5 avec PHP-FPM, rien de plus facile:

```
$ apt-get install php5-fpm
```

## [](#installation-des-modules-php5)Installation des modules PHP5

Pour pouvoir gérer la plupart fonctionnalités de vos sites tranquillement, vous devez installer les modules usuels de PHP (notamment pour le support mysql pour PHP):

```
apt-get install php5-mysql php-apc php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-sqlite php5-xmlrpc php5-xsl php5-xcache
```

Adaptez la commande à vos propres besoins. Puis rechargez PHP5-FPM.

## [](#installation-de-phpmyadmin)Installation de phpMyAdmin

MySQL, c'est cool, mais bon en ligne de commande moi je trouve ça chiant donc on va installer phpMyadmin.

```
apt-get install phpmyadmin
```

Il va vous demander quel serveur reconfigurer automatiquement. C'est bête il ne propose que apache ou lighttpd donc on ne coche rien et on valide.

Ensuite il va vous demander si il doit configurer ou non la base de données pour phpmyadmin, mettez "oui" ou "yes", tapez le mot de passe MySQL de l'utilisateur root (celui que je vous ai dit de noter au début). Validez, il va vous demander un second mot de passe. Pour celui-là vous n'êtes pas obligés de rentrer quelque chose, le mot de passe sera généré automatiquement.

À présent, on va devoir configurer un vhost pour pouvoir accéder à phpMyAdmin depuis un navigateur. Ouvrez le fichier

```
/etc/nginx/sites-available/default
```

pour y insérer les lignes suivantes, à l'intérieur de la partie `server {},` comme ceci:

```
server {
...

    location /phpmyadmin {
        root /usr/share/;
        index index.php index.html index.htm;

        location ~ ^/phpmyadmin/(.+\.php)$ {
            try_files $uri =404;
            root /usr/share/;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include /etc/nginx/fastcgi_params;
        }

        location ~* ^/phpmyadmin/(.+\.(jpg|jpeg|gif|css|png|js|ico|html|xml|txt))$ {
            root /usr/share/;
        }
    }

    location /phpMyAdmin {
        rewrite ^/* /phpmyadmin last;
    }
}
```

Relancez NGINX:

```
$ service nginx reload
```

Et accédez depuis votre navigateur à _[http://adresse.devoreserveur.com/phpmyadmin](http://adresse.devoreserveur.com/phpmyadmin)_. Si phpMyAdmin s'affiche, bravo. Connectez-vous avec les identifiants MySQL root que vous avez crées au début.

Allez, il reste plus qu'une seule étape et on a fini.

## [](#installation-de-pureftpd-mysql)Installation de PureFTPd MySQL

Lancez l'installation classique:

```
$ apt-get install pure-ftpd-mysql
```

Puis créez l'utilisateur Unix

```
ftpuser
```

, ainsi que le groupe Unix

```
ftpgroup
```

. Ils serviront de passerelle à tous les comptes FTP que vous créerez via PureFTPd.

```
$ groupadd -g 2001 ftpgroup
$ useradd -u 2001 -s /bin/false -d /bin/null -c "PureFTPd user" -g ftpgroup ftpuser
```

À présent, il faut créer une base de donnée pour pouvoir administrer nos comptes FTP. On peut le faire depuis phpMyAdmin mais histoire d'aller un peu plus vite je vous donne les instructions en ligne de coommande:

```
$ mysql -u root -p
CREATE DATABASE pureftpd;
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP ON pureftpd.* TO 'pureftpd'@'localhost' IDENTIFIED BY 'ftpdpass';
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP ON pureftpd.* TO 'pureftpd'@'localhost.localdomain' IDENTIFIED BY 'ftpdpass';
FLUSH PRIVILEGES;
```

Il y a 5 commandes:

- la 1ère pour se connecter à MySQL
- la seconde crée la base de données
- la 3ème cet 4ème créent l'utilisateur MySQL _pureftpd_. Remplacez "ftpdpass" dans la commande par un mot de passe de votre choix
- la 5ème recharge les privilièges

Ensuite, toujours dans la l'invite de commande MySQL:

```
USE pureftpd;
```

```
CREATE TABLE ftpd (
User varchar(16) NOT NULL default '',
status enum('0','1') NOT NULL default '0',
Password varchar(64) NOT NULL default '',
Uid varchar(11) NOT NULL default '-1',
Gid varchar(11) NOT NULL default '-1',
Dir varchar(128) NOT NULL default '',
ULBandwidth smallint(5) NOT NULL default '0',
DLBandwidth smallint(5) NOT NULL default '0',
comment tinytext NOT NULL,
ipaccess varchar(15) NOT NULL default '*',
QuotaSize smallint(5) NOT NULL default '0',
QuotaFiles int(11) NOT NULL default 0,
PRIMARY KEY (User),
UNIQUE KEY User (User)
) ENGINE=MyISAM;

quit;
```

Cela va crée la table responsable des comptes utilisateurs. C'est bientôt fini, il ne reste plus qu'à configurer PureFTPd et à créer un utilisateur.

### [](#configuration-de-pureftpd)Configuration de PureFTPd

Éditez le fichier `/etc/pure-ftpd/db/mysql.conf`:

```
$ cp /etc/pure-ftpd/db/mysql.conf /etc/pure-ftpd/db/mysql.conf_orig
$ cat /dev/null > /etc/pure-ftpd/db/mysql.conf
$ vim /etc/pure-ftpd/db/mysql.conf
```

et insérez-y les lignes suivantes:

```
MYSQLSocket /var/run/mysqld/mysqld.sock
#MYSQLServer localhost
#MYSQLPort 3306
MYSQLUser pureftpd
MYSQLPassword ftpdpass
MYSQLDatabase pureftpd
#MYSQLCrypt md5, cleartext, crypt() or password() - md5 is VERY RECOMMENDABLE uppon cleartext
MYSQLCrypt md5
MYSQLGetPW SELECT Password FROM ftpd WHERE User="\L" AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
MYSQLGetUID SELECT Uid FROM ftpd WHERE User="\L" AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
MYSQLGetGID SELECT Gid FROM ftpd WHERE User="\L"AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
MYSQLGetDir SELECT Dir FROM ftpd WHERE User="\L"AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
MySQLGetBandwidthUL SELECT ULBandwidth FROM ftpd WHERE User="\L"AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
MySQLGetBandwidthDL SELECT DLBandwidth FROM ftpd WHERE User="\L"AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
MySQLGetQTASZ SELECT QuotaSize FROM ftpd WHERE User="\L"AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
MySQLGetQTAFS SELECT QuotaFiles FROM ftpd WHERE User="\L"AND status="1" AND (ipaccess = "*" OR ipaccess LIKE "\R")
```

Penez à remplacer _ftppass_ (la 5ème ligne) par le mot de passe que vous avez choisi dans l'étape précédente.

Ensuitem exécutez les commandes suivantes, qui vont créer des fichiers de configuration:

```
$ echo "yes" > /etc/pure-ftpd/conf/ChrootEveryone
$ echo "yes" > /etc/pure-ftpd/conf/CreateHomeDir
$ echo "yes" > /etc/pure-ftpd/conf/DontResolve
```

La première commande va permettre de confiner chaque utilisateur dans le dossier qui lui est attribué, pour éviter qu'il ne puisse lister tous les fichiers du serveur. La deuxième permet de créer automatiquement un dossier utilisateur si il n'en pas par défaut. Enfin la 3ème et dernière commande permet d'accélerer sensiblement le service FTP.

Il en vous reste plus qu'à redémarrer PureFTPd:

```
$ service pure-ftpd-mysql restart
```

Et voilà ! Vous avez à présent un beau petit serveur web tournant avec Nginx, php5-fpm, MySQL, phpmyadmin et faisait aussi serveur FTP avec PureFTPD.

Si vous avez des questions ou des remarques, n'hésitez pas à m'en faire part dans les commentaires.

**Sources**: [http://www.howtoforge.com/installing-nginx-with-php5-and-php-fpm-and-mysql-support-lemp-on-ubuntu-12.10](http://www.howtoforge.com/installing-nginx-with-php5-and-php-fpm-and-mysql-support-lemp-on-ubuntu-12.10) [http://www.howtoforge.com/running-phpmyadmin-on-nginx-lemp-on-debian-squeeze-ubuntu-11.04](http://www.howtoforge.com/running-phpmyadmin-on-nginx-lemp-on-debian-squeeze-ubuntu-11.04) [http://www.howtoforge.com/virtual-hosting-with-pureftpd-and-mysql-incl-quota-and-bandwidth-management-on-ubuntu-12.04](http://www.howtoforge.com/virtual-hosting-with-pureftpd-and-mysql-incl-quota-and-bandwidth-management-on-ubuntu-12.04)
