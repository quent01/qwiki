
# PlatformSH-QT

## Appréhension de l'outils Platform SH

Démarche pour faire fonctionner un site sur plaform.sh, commandes importantes et notions à avoir.

### Mise en place d'un dépot fonctionnant avec Platform.sh

- Créer un dépot tournant sous une box vagrant (le provisionning doit installer une clé SSH et mettre a jour composer)
- Créer un projet dans platform.sh
- Dans le paramétrage de votre compte aller dans "account settings" > "SSH KEYS" (renseigner la clé publique de la clé qui s'est installé sur votre box ```/home/vagrant/.ssh/id_rsa.pub``` et votre clé à vous ```C:\Users\<username>\.ssh\id_rsa.pub```(optionnel)
- Créer votre fichier ```.platform.app.yaml``` à la racine de votre projet 
- Créer le dossier ```.plateform``` à la racine de votre projet contenant
    - ```config.yaml```
    - ```routes.yaml```
    - ```services.yaml```
- créer un ```composer.json``` avec en require-dev platformsh/cli
- via vagrant ssh faite un composer install
- sur [Bitbucket](https://bitbucket.org) dans le dépot aller dans "Paramètres" > "Platform.sh integration" et connecter vous à votre projet platform.sh.

### Déploiement du dépot

- Suivant le type de projet sous lequel on est platform ne gère pas les choses de la même façon, la notion la plus interessante à retenir c'est que pour la connexion a la BDD c'est lui qui fournit les infos via une variable d'environnement (regarder le fichier ```public/config/database.php``` pour l'exemple)
    - pour les CMS ou frameword, c'est platform qui va générer le fichier de connexion BDD; pour ce genre de projet bien commencer avec les templates que fournit PLATEFORMSH sur leur dépot GIT https://github.com/platformsh; perso j'utilise l'outil [Astral](https://app.astralapp.com) pour garder des dépots que j'aime bien (il suffit de "star" le dépot, on peut ensuite les ranger par tag)
- On utilise l'outil plateform-cli pour faire les actions de dump, rsync sur les fichiers (/vendor/bin/platform <commande>)
- les endroit ou on veut que les droit d'ecriture soit présent doivent être dans le section "mount" du ```.platform.app.yaml```
- c'est seulement lors du build les fichiers sont dispo en écriture sinon tout est juste en lecture à l'exception de ce qui est dans mount. (on ne peut pas du coup se connecter sur la prod pour editer des fichiers)
```
# dans le cas ou il faut juste lancer le redeploiement sans rien changer (a cause d'un plantagepar exemple)
vendor/bin/platform redeploy
```


### La doc à retenir

- la structure de platform.sh (3 branches dispo en live) : https://docs.platform.sh/overview/structure.html
- Je push un commit que se passe t'il (Ma branche est buildé et déployé) : https://docs.platform.sh/overview/build-deploy.html
- https est dispo de base (le mettre du coup dans routes.yaml)
- ce qu'il faut retenir coté BDD (info de connexion dispo via ```getenv('PLATFORM_RELATIONSHIPS')```) : https://docs.platform.sh/configuration/services/mysql.html
- Platform place le dépot dans un répertoire app/

Commandes platform à retenir :

```
# liste des environnements
vendor/bin/platform environment:list

# Envoyer les fichiers sur la prod 
vagrant ssh 
cd /var/www/ 
rsync -az public/sites/default/files/ `vendor/bin/platform ssh --pipe`:public/sites/default/files/ 
Choisir le dépot puis la branche 

# Récupérer la bdd de prod
vendor/bin/platform db:dump

# Envoyer une BDD sur "branch_name"   
- vendor/bin/platform sql --project=[project_id] -e [branch_name] < db.xxxx.xx.xx.sql 
- préciser dans le fichier de configuration platform le prefix s'il existe 

# Connaitre IP du NDD 
vendor/bin/platform environment:info edge_hostname
# ping du resulat

# Get uploads 
platform mount:list
platform mount:download

# dans le cas ou il faut juste lancer le redeploiement sans rien changer (a cause d'un plantagepar exemple)
vendor/bin/platform redeploy

# clear build cache
vendor/bin/platform project:clear-build-cache
```
- Faire des snapshot : https://docs.platform.sh/administration/snapshot-and-restore.html (intégré la tache cron en exemple dans le ```.platform.app.yaml```) 
 
 
## Fonctionnement d'un Drupal sur platform SH 
 
spécifique à Drupal : si on choisit dans platform.app.yaml le "build flavor : drupal", il ne faut pas avoir de fichier *.make ou *.project à la racine du site afin qu'il ne prenne que les fichiers du repo en compte 
On va tester le dépot en faisant fonctionner www.energem.fr sur platform.sh 

## Questions qu'il reste a répondre

- comment lier un nom de domaine (on veut accéder à master via une url bien précise) ? : je pense il faut utiliser {all} à la place de {default} dans le route.yaml
- accès FTP ? 
- préconfigurer le projet pour le dépot (ex. lors d'un rsync ou de l'envoi de la bdd, ne pas avoir à préciser l'ID du projet)
 
## TODO LIST 
- envoyer les fichiers (sites/default/files) => OK 
- builder le css/js => OK
- régler les NDD (energem.tiz.fr) => OK
- vérifier si le site fonctionne, faire les tests de deploiements sur les différents environnements => OK
- modifier le max_input_vars, memory_limit (apache) et max_allowed_packet (mysql) => OK