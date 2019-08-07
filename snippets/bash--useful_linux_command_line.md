# GREP
```
grep -rli "word" .
```
Recherche "word" dans l'arboresence à partir de "."
- "-r" : recursive
- "-i" : ne tiens pas compte de la casse

# FIND
```
# find file superior at 3000k from .
find . -type f -size +3000k
```

# MYSQL
```
mysqldump -u USERNAME -p DB_NAME > filename.sql
mysqldump -h HOSTNAME -u USERNAME -p DB_NAME > filename.sql
mysql -u USRNAME -p DB_NAME < filename.sql

ou 

/usr/local/mysql/bin/mysqldump -u USRNAME -pPASSWORD DB_NAME > dumpfilename.sql
/usr/local/mysql/bin/mysql -u USRNAME -pPASSWORD DB_NAME < dumpfilename.sql

```

# RSYNC
+ rsync -arv entree/ destination/
    - "-a" : conserve les info sur les fichiers : dates,etc
    - "-v" : verbose
    - "-z" : transfert en compressant les données
    - "-r" : recursive
    - "-p" : garde les permissions
    - Le '/' est important, sinon le dossier parent est copié
Exemple pour syncroniser via SSH
```
cd destination
rsync -arvz -e ssh admin@www.moto-vision.com:/d_moto-vision-s/www/www.moto-vision.com/htdocs/ .
```

# CHMOD
## Change CHMOD to 644 on all files
```
find ./ -type f -exec chmod 644 {} +
```

## Change CHMOD to 755 on all folder
```
find ./ -type d -exec chmod 755 {} +
```

# TAR GZ
Effectuer un tar gz en excluant les dossier folder et upload/folder
```
tar --exclude "./public/vendor" --exclude "./public/web/modules/contrib" -cvzf chr.local.2019.01.31.tar.gz ./public 
```

# SSH KEY
## Générer une clé SSH
```
ssh-keygen -t rsa
```
## Envoyer sa clé SSH sur un serveur
```
cat ~/.ssh/id_rsa.pub | ssh <user>@<server_name> "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
```

# LIEN SYMBOLIQUE
Sur certain serveur (comme tizix ou creatiz), on peut créer un lien symbolique entre dossier.
Pour créer un lien symbolique d'un dossier1 vers un dossiersrc, où l'on souhaite lorsque l'on rentre dans
dossier1 avoir le contenu de dossierSRC, la commande est la suivante : 
```
ln -a dossierSRC dossier1
```

# Encodage
Si git est installer sur votre PC il est possible de voir l'encodage des fichiers, piur ça aller dans le repertoire ou vous souhaitz voir l'encodage et faite
```
file *
```

# Administration serveur
## Conaitre la distribution Linux
```
cat /etc/os-release
```

## Connaitre la quantité de mémoire
```
free -m
free -m | grep -i mem | awk '{ print $2" MB" }'
```

## Espace disque
```
df -h
```

## Nombre de processeurs
```
cat /proc/cpuinfo
```

## Version de php
```
php -v
php -i
```

## Determine the virtualisation type
```
lscpi
dmesg|head -500
```

# Mail
## Voir si les mails sont en queue
Cela  arrive quand le serveur en face les refuse/delay
Pour infos les log de qmails sont situé dans /home/log/qmail
```
qmailctl stat
```

# Telnet
```
telnet <nom_machine>
```