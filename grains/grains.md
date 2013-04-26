!SLIDE
# Grains

Les grains sont des caractéristiques d'un client (mémoire totale, OS...) :

```bash
$ sudo salt 'coruscant*' grains.ls
coruscant:
    - biosreleasedate
    - biosversion
    - cpu_flags
    - cpu_model
    - cpuarch
    - defaultencoding
    - defaultlanguage
    - domain
    - fqdn
    - gpus
    - host
    - id
    - ipv4
    - kernel
    ...
```

!SLIDE
# Exemple


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
# Ciblage

```bash
$ sudo salt -G 'os:RedHat' test.ping
```
