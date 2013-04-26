!SLIDE
# pillar

Interface pour distribuer des donnés sur l'ensemble des clients :

```jinja
{% if grains[’os’] == ’RedHat’ %}
    apache: httpd
    git: git
{% elif grains[’os’] == 'Ubuntu' %}
    apache: apache2
    git: git-core
{% endif %}
```

!SLIDE
# Pillar

Définitation qui peut ensuite être utilisées :

```yaml
apache:
  pkg:
    - installed
    - name: {{ pillar[’apache’] }}
git:
  pkg:
    - installed
    - name: {{ pillar[’git’] }}
```
