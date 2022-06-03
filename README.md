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

awk '($9 ~ /404/)' /car/loghttpd/access_log | awk '{print $9,$7}' | sort | sed -n '/404$/p' | \ awk '{print $1}' | tail -f; do iptables -A INPUT -s $1 -j DROP |
crontab -r $3;
done

```
