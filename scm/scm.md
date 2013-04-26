!SLIDE
# Pourquoi un SCM ?

Les outils SCM est un gros pas en avant en simplifiant grandement le travail d'administration. 

!SLIDE
# Qualité


* Configuration as Code
* Configuration as Documentation
* Plus proche du développement (outil, langage, etc)
* Langage commun (DSL)
* Flexible
* Rapidité
* Idempotence
* Abstraction

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
# Critères

Choix d'une solution selon :

* Qualité de la documentation
* Courbe d'apprentissage
* Simplicité

!SLIDE
# Puppet

* Trés utilisé
* Beaucoup de documentation
* Footprint assez important (Ruby)
* DSL pas très compliqué (JSON-like)
* Orienté système
* Racheté par VMWare
* J'ai trouvé ça assez compliqué à configurer
* Pas mal de soucis sécu les derniers mois
* Pas très rapide (ne scale pas très bien)

!SLIDE
# Chef

* Footprint assez important (Ruby, Erlang)
* Architecture trop compliquée (PostgreSQL, Solr, Erlang, Ruby...)
* DSL compliqué (sous ensemble Ruby) et potentiellement illisible
* Non orienté système
* Impératif et non déclaratif

!SLIDE
# CFEngine

* Footprint très bas (C)
* Robuste, sécurisé, bien conçu
* Doc super mal foutu
* Site trop orienté commercial à mon goût
* Syntaxe compliquée
* Très bonne scalabilité
* Version commerciale avec beaucoup de fonctionnalités