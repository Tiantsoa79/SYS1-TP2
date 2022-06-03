# BLOQUER LES CRAWLERS SUR APACHE2

Aller dans le dossier log d'Apache

```
cd /var/log/apache2
```

Créer le fichier qui va s'occuper du blocage 

```
nano blocking.sh
```

Entrer le script suivant : 

```
#!/bin/sh

awk '($9 ~ /404/)' /var/log/httpd/access_log | awk '{print $9,$7}' | sort | sed -n '/404$/p' | \ awk '{print $1}' | tail -f; do iptables -A INPUT -s $1 -j DROP |
crontab -r $3;
done

```

Explications des étapes :

awk '($9 ~ /404/)' : récupère toutes les requêtes 404 dans access_log
awk '{print $9,$7}' : récupère les requêtes avec leurs IP
sort : effectue un tri
sed -n '/404$/p' : filtre avec précision des requêtes 404
\ awk '{print $1}' : récupère l'IP
tail -f : affiche chaque ligne
do iptables -A INPUT -s $1 -j DROP : bloque les IP en question
crontab -r $3 : bloque les utilisateurs
