!SLIDE
# Résumé

SaltStack est à la fois :

* un outil de gestion de configuration (SCM)
* un shell distribué.

http://saltstack.com/

Licence Apache 2.0

!SLIDE
# Ce que j'ai tout de suite apprécié

* Tutorial "5 minutes"
* Installation facile (PPA Ubuntu)
* Documentation simple et complète (900 pages)
* 200 modules
* Le shell

!SLIDE
# Technologie

* Python
* YAML (configuration)
* msgpack (format de communication)
* ZeroMQ (communication)
* AES (chiffrage)

!SLIDE
# Installation Ubuntu

```bash
$ sudo add-apt-repository ppa:saltstack/salt
$ sudo aptitude update
$ sudo aptitude install salt-master salt-minion
```

!SLIDE
# 1ere utilisation

Coté client (Minion) :

* Configuration de l'ip du serveur
* Lancement
* Génère automatiquement son certificat
* Tente périodiquement de se connecter au serveur

Coté serveur :

* Accepter la clé (salt-key -A)
* Test (salt '*' test.ping)

!SLIDE
# Canaux de communication

Ports :

* 4505 (PUB)
* 4506 (REQ)

!SLIDE
# Ciblage

Le ciblage est la sélection des clients

```bash
salt '*' test.ping
salt ’*.example.net’ test.ping
salt ’web?.example.net’ test.ping
salt ’web[1-5]’ test.ping
salt -E ’web1-(prod|devel)’ test.ping
salt -L ’web1,web2,web3’ test.ping
salt -G ’os:CentOS’ test.ping
salt -G ’cpuarch:x86_64’ grains.item num_cpus
```
Mode batch :

```bash
salt '*' -b 10 test.ping
salt -G 'os:Redhat' --batch-size 25% test.ping
```

Note : un mode schedeling existe.

!SLIDE
# Module / Fonction

Appel de la fonction X du module Y :

```bash
salt '*' test.ping
salt '*' cmd.run ls '/'
salt ’*’ cmd.exec_code python 'import sys; print sys.version'
salt ’*’ pip.install salt timeout=5 upgrade=True
```