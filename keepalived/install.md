Install prerequisites.
```bash
apt install libipset13
```

Install keepalived.
```bash
apt install keepalived
```

Configure nodes.
```bash
nano /etc/keepalived/keepalived.conf
```

Enable service.
```bash
systemctl enable --now keepalived.service
```
