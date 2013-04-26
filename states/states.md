!SLIDE
# SaltStack States (SLS)

Fichier contenant des états cibles, constitué de :

* dictionnaire
* liste
* chaine de caractères
* nombre

!SLIDE
# renderer

Plusieurs sérialisation possible :

* Jinja + YAML (défaut) / JSON
* Mako + YAML / JSON
* Wempy + YAML / JSON
* pydsl
* pur Python

!SLIDE
# Exemples simples

```yaml
vim:
  pkg.installed

/etc/vimrc:
  file:
    - managed
    - source: salt://vimrc
    - mode: 644
    - user: root
    - group: root
    - template: jinja

apache:
  pkg:
    - installed
  service:
    - running
    - require:
      - pkg: apache
```

Puis on lance la commande :

```bash
$ sudo salt '*' state.highstate

!SLIDE
# Top SLS

```bash
base:
  ’*’:
    - common
    - user.admin

  'web':
    - nginx
    - postgresql
```

!SLIDE
# Environement

On specifie un environnement dans la configuration du serveur :

```bash
file_roots:
  base:
    - /srv/salt
```

Ou plusieurs : 

```bash
file_roots:
  base:
    - /srv/salt/base
  dev:
    - /srv/salt/dev
  qa:
    - /srv/salt/qa
  prod:
    - /srv/salt/prod
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


failhard (local ou global)

En impératif ou déclaratif (option state_auto_order)

!SLIDE
# YAML + Jinja2

http://jinja.pocoo.org/docs/

Jinja2 est un outil de templating Python simple & puissant :

```python
{% for usr in 'toto','titi','tutu' %}
{{ usr }}:
  user.present
{% endfor %}
```

!SLIDE
# Formula

https://github.com/saltstack-formulas

On ajoute des formulas avec l'option gitfs_remotes (ou clonage à la main).

Installation d'OpenStack sur une machine :

```bash
base:
  'myopenstackmaster':
    - openstack
```

!SLIDE
# Serveur de fichier

Salt contient un serveur de fichier (serveur ZeroMQ). Plusieurs Backend :

* FS (défaut)
* git

```bash
# salt '*' cp.get_file salt://vimrc /etc/vimrc
# salt '*' cp.get_file "salt://{{grains.os}}/vimrc" /etc/vimrc template=jinja
```
