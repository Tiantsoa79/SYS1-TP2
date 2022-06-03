# BLOQUER LES CRAWLERS SUR APACHE2

###Aller dans le dossier log d'Apache

```
cd /var/log/apache2
```

###Créer le fichier qui va s'occuper du blocage 

```
nano blocking.sh
```

###Entrer le script suivant : 

```
#!/bin/sh

awk '($9 ~ /404/)' /var/log/httpd/access_log | sed -n '/404$/p' | tail -f; do iptables -A INPUT -s $1 -j DROP |
crontab -r $3;
done

```

###Explications des étapes :

•**awk '($9 ~ /404/)'** : affiche le 9eme résultat de toutes les requêtes 404 dans access_log

•**sed -n '/404$/p'**: filtre avec précision les requêtes 404

•tail -f : affiche chaque ligne

•do iptables -A INPUT -s $1 -j DROP : bloque les IP

•crontab -r $3  : bloque les utilisateurs
