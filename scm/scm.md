!SLIDE
# Pourquoi un SCM ?

Les outils SCM est un gros pas en avant en simplifiant grandement le travail d'administration. 

!SLIDE
# Qualité

* Configuration as Code
* Plus proche du développement (outil, langage, etc)
* Configuration as Documentation
* Langage commun (DSL)
* Flexible
* Rapidité
* Abstraction
* Idempotence

!SLIDE
# Solutions

* Puppet
* Chef
* CFEngine
* Bcfg2
* Juju
* Ansible
* Fabric
* ...

!SLIDE
# Critères personnels

Mon choix d'une solution selon :

* Qualité de la documentation
* Courbe d'apprentissage
* Simplicité

!SLIDE
# Puppet ?

«Avantages» :

* Trés utilisé
* Beaucoup de documentation
* Orienté système

«Defauts » :

* Footprint assez important (Ruby)
* trop compliqué à configurer à mon gout
* Pas mal de soucis sécu les derniers mois
* Pas très rapide (et ne scale pas très bien)

!SLIDE
# Chef ?

«Avantages» :

* Permet de définir précisemment son workflow

«Defauts » :

* Footprint assez important (Ruby, Erlang)
* Architecture trop compliquée (PostgreSQL, Solr, Erlang, Ruby...)
* DSL compliqué (sous ensemble Ruby) et potentiellement illisible
* Non orienté système

!SLIDE
# CFEngine ?

«Avantages» :

* Footprint très bas (C)
* Robuste, sécurisé, bien conçu
* Très bonne scalabilité

«Defauts » :

* Open-core
* Doc super mal foutu
* Site trop orienté commercial à mon goût
* Syntaxe compliquée