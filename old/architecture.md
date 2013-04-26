!SLIDE
# Résumé

SaltStack est à la fois :

*un outil de gestion de configuration (software configuration management ou SCM)
*un shell distribué.

Licence Apache 2.0

!SLIDE
# Ce que j'ai apprécié

* Documentation simple et complète (700 pages)
* Prêt en 2 minutes (PPA Ubuntu)
* Le shell

!SLIDE
# Technologie

* Python
* YAML (configuration)
* msgpack (format de communication)
* ZeroMQ (communication)
* AES (chiffrage)

!SLIDE
# Communication

Au lancement du Minion (client) :

* Génère sa clé (si 1er lancement)
* Tente de se connecter au serveur

Coté serveur :
* Accepter la clé

Ports :

* 4505 (PUB)
* 4506 (REQ)

!SLIDE
# SaltStack States (SLS)

Fichier contenant un état cible, constitué de :

* dictionnaire
* liste
* chaine de caractère
* nombre

Plusieurs sérialisation possible (renderer) :

* Jinja + YAML (défaut) / JSON
* Mako + YAML / JSON
* Wempy + YAML / JSON
* pur Python
* pydsl


!SLIDE
# Vocabulaire

* Grains (données statiques sur le client)
* Pillar (état cible)
* State (appel de fonctions)

=> utilisé par le composant Salt States

!SLIDE
# Serveur de fichier

Salt contient un serveur de fichier (serveur ZeroMQ). Plusieurs Backend :

* FS (défaut)
* git

!SLIDE
# Exemple simple

```
vim:
  pkg.installed

/etc/vimrc:
  file.managed:
    - source: salt://vimrc
    - mode: 644
    - user: root
    - group: root
```

Puis on lance la commande :

```bash
$ salt '*' state.sls nginx # ou salt '*' state.highstate
```

!SLIDE
# Dépendance et lien

On peut inclure ou étendre des définitions : 

* include
* extend

Il existe aussi la notion de dépendance :

* require / require_in
* watch / watch_in
* use
* failhard (local ou global)

!SLIDE
# YAML + Jinja2

http://jinja.pocoo.org/docs/

Jinja2 est un outil de templating Python simple & puissant :

```python
{% for usr in 'moe','larry','curly' %}
{{ usr }}:
  user.present
{% endfor %}
```

!SLIDE
# rendu py

Quand le format YAML n'est pas assez expressif, on utilile le rendu py :

```python
#!py

def run():
    '''
    Install the django package
    '''
    return {'include': ['python'],
            'django': {'pkg': ['installed']}}
```

!SLIDE
# rendu pydsl

Ou alors avec le rendu pydsl :

```python
#!pydsl

include('python', delayed=True)
state('django').pkg.installed()
```
!SLIDE
# Grains

Les grains sont des caractéristiques d'un client (mémoire totale, OS...) :

```python
apache:
  pkg.installed:
    {% if grains['os'] == 'RedHat' %}
    - name: httpd
    {% elif grains['os'] == 'Ubuntu' %}
    - name: apache2
    {% endif %}
```

!SLIDE
# Modules Salt

SaltStack contient environ 130 modules dont :

* cmd / cron / iptables / mount / pam / ps
* pkg / sys / apt / brew / pip / gem / systemd
* apache / nginx / kvm / postgres / rabbitmq
* git / hg / svn
* monit / puppet 

!SLIDE
# Modules Salt

L'écriture d'un module est très simple si on connait Python car un module
Salt est tout simplement un module Python.

* En posant le module dans le répertoire $file_roots/_modules, il est 
  automatiquement synchroniser avec les Minions (clients).
* Les modules peuvent s'appeler entre eux avec la variable __salt__
* Il existe des paquets virtuels (exemples : apt, yumpkg)



# salt '*' cp.get_file salt://vimrc /etc/vimrc
# salt '*' cp.get_file "salt://{{grains.os}}/vimrc" /etc/vimrc template=jinja

!SLIDE
# Reactor

Capacité de Salt à éxécuter des commandes selon des évènements.

!SLIDE
# shell distribué

Tous les modules Salt sont accessibles en ligne de commande !

!SLIDE
# Cibles

On peut choisir une cible de plusieurs manières :

* PCRE
* glob
* grains
* alias

Exemples :

```bash
$ salt '*foo.com' sys.doc
$ salt -E '.*' cmd.run 'ls -l | grep foo'
$ salt -L foo.bar.baz,quo.qux cmd.run 'ps aux | grep foo'
$ salt -G 'os:Fedora' test.ping
$ salt -N 'webserver' test.ping
$ salt -I 'role:production*' test.ping
$ salt -S '192.168.10.0/24' test.ping
```

!SLIDE
# Taille du batch

On peut choisir la taille du batch :

```bash
$ salt '*' -b 10 test.ping
$ salt -G ’os:RedHat’ --batch-size 25% apache.signal restart
```

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
# Scheduling

On peut éxécuter des états à intervalles réguliers.

!SLIDE
# Returner

Un «returner» est un «connecteur».

Un certain nombre intégré par défaut :

* carbon_return
* cassandra_return
* local
* mongo_future_return
* mongo_return
* mysql
* postgres
* redis_return
* sentry_return
* smtp_return
* syslog_return

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

import salt.utils.event
event = salt.utils.event.MasterEvent('/var/run/salt/master')
data = event.get_event(wait=10, tag='auth')

!SLIDE
# Backup

On peut configurer un backup pour ne pas effacer les fichiers gérés
(file.managed ou file.recursive).

!SLIDE
# Syndic

Proxy qui se connecte au master pour retransmettre des commandes.

!SLIDE
# Masterless

On peut utiliser Salt en local :

```bash
# salt-call cmd
```

!SLIDE
# API Python

Salt est programmable en Python : 

```python
# Import the Salt client library
import salt.client

# create a local client object
client = salt.client.LocalClient()

# make calls with the cmd method
ret = client.cmd('*', 'cmd.run', ['ls -l'])
```

!SLIDE
# salt-api

Librairie qui expose une API.

!SLIDE
# Cloud

La version 0.14 apporte la possibilité de maitriser des VMs :

* Amazon EC2
* Eucalyptus (using EC2)
* OpenStack
* Rackspace (using OpenStack)
* HP Cloud (using OpenStack)
* GoGrid
* Joyent
* Linode
* Parallels
* DigitalOcean
