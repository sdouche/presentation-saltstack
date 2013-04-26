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

https://github.com/saltstack/salt-api

Librairie qui expose une API au dessus de Salt pour fournir une variété de points d'entrée (REST, XMLRPC, Websocket, WSGI...).