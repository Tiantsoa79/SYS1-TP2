# BLOQUER LES SCRAWLERS SUR APACHE2 
(En une ligne)

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
