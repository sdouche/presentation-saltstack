!SLIDE
# Sortie

On peut choisir de récupérer les infos en :

* no_return
* grains
* yaml
* overstatestage
* json
* pprint
* nested
* raw
* highstate
* quiet
* key
* txt
* virt_query

!SLIDE
# Returner

Un «returner» est un «connecteur».

Un certain nombre intégré par défaut :

* carbon
* cassandra
* local
* mongo
* mysql
* postgres
* redis
* sentry
* smtp
* syslog

!SLIDE
# peer communication

Il est possible de configurer les clients pour retransmettre des commandes.

```
peer:
  .*example.com:
    - test.*
    - ps.*
    - pkg.*
  .*foo.org:
    - test.*
    - ps.*
    - pkg.*
```

!SLIDE
# ACL

```
client_acl:
  fred:
    - web\*:
      - pkg.list_pkgs
      - test.*
      - apache.*
```

On peut déléguer les ACLs à une authentification externe (avec ou sans jetons).

!SLIDE
# Gestion des jobs

Salt maintient une liste des tâches :

```bash
$ salt-run jobs.active
$ salt-run jobs.list_jobs
```

!SLIDE
# Gestion des événements

```python
import salt.utils.event
event = salt.utils.event.MasterEvent('/var/run/salt/master')
data = event.get_event(wait=10, tag='auth')
```

Vous pouvez envoyer des logs sur Sentry ou Logstash.

!SLIDE
# Backup

On peut configurer un backup pour ne pas effacer les fichiers gérés
(file.managed ou file.recursive).

!SLIDE
# Masterless

On peut utiliser Salt en local :

```bash
$ sudo salt-call cmd
```