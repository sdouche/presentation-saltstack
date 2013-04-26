!SLIDE
# Modules Salt

SaltStack contient environ ~200 modules :

* cmd / cron / iptables / mount / pam / ps
* pkg / sys / apt / brew / pip / gem / systemd
* apache / nginx / kvm / postgres / rabbitmq
* git / hg / svn
* monit / puppet 

Il existe des paquets virtuels (exemples : pkg, user, group, service).

!SLIDE
# Modules Salt

L'écriture d'un module est très simple si on connait Python car un module
Salt est tout simplement un module Python.

* Automatiquement synchroniser en posant le module dans $file_roots/_modules
* Les modules peuvent s'appeler entre eux avec la variable __salt__

!SLIDE
# Exemple de code

```python

import sys
import time
import random

import salt
import salt.version
import salt.loader


def echo(text):
    '''
    Return a string - used for testing the connection

    CLI Example::

        salt '*' test.echo 'foo bar baz quo qux'
    '''
    return text


def ping():
    '''
    Just used to make sure the minion is up and responding
    Return True

    CLI Example::

        salt '*' test.ping
    '''
    return True
 ```
