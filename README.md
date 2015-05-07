Ansible Consul
---

This will lauch 5 ubuntu hosts with consul installed and ther service run under supervisord.

Currently under heavy testing.

Launch:
---
```$ vagrant up```

SSH:
---
```$ vagrant ssh consul1```


Consul:
---

Check that consul is running:

```
$ sudo consul members
consul1  172.16.10.1:8301  alive   server  0.5.0  2
consul2  172.16.10.2:8301  alive   server  0.5.0  2
consul4  172.16.10.4:8301  alive   client  0.5.0  2
consul5  172.16.10.5:8301  alive   client  0.5.0  2
consul3  172.16.10.3:8301  alive   server  0.5.0  2
```

You can drop service files into ```/etc/consul.d/``` and restart supervisord with:
```
$ sudo supervisorctl restart consul
consul: stopped
consul: started
```


If consul isn't running try:
```
$ /usr/local/bin/consul agent -config-dir /etc/consul.d
```

Check consul out:
---
[key value store](https://www.consul.io/docs/agent/http/kv.html)
[health checks](https://www.consul.io/docs/agent/http/health.html)

more at [consul](https://www.consul.io/docs)
