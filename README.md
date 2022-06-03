# BLOQUER LES SCRAWLERS SUR APACHE2 
(En une ligne de script)

Les termes de crawler, robot de crawl ou spider, désignent dans le monde de l'informatique un robot d'indexation. Concrètement, il s'agit d'un logiciel qui a pour principale mission d'explorer le Web afin d'analyser le contenu des documents visités et les stocker de manière organisée dans un index.
Pour les bloquer, suivez les étapes suivantes : 

### Aller dans le dossier log d'Apache

```
cd /var/log/apache2
```

### Créer le fichier qui va s'occuper du blocage 

```
nano blocking.sh
```

### Entrer le script suivant : 

```
#!/bin/sh

cat /var/log/apache2/access.log | grep 'spider\|bot' | sed 's/[^\/]*/\./;s/].*$//g' | awk '{print $1}' | uniq | sort | tail -n 100 | iptables -A INPUT $1 -j REJECT;

```

Ceci permet à la fois d'afficher (cat), de filtrer (grep), de récupérer(des, awk)(plus les paramètres de tri et de regroupement en adresse IP unique(uniq, sort, tail), et de rejeter les requêtes des IP des scrawlers (avec iptables).

#### il suffit ensuite de donner les droits sur le script

```
chmod +x blocking.sh
```
#### et de l'exécuter
```
./blocking.sh
```
