Install prerequisites on Master and Backup nodes.
```bash
apt install libipset13
```

Install keepalived on Master and Backup nodes.
```bash
apt install keepalived
```

Configure Master and Backup nodes. Refer to Master and Backup keepalived.conf files.
```bash
nano /etc/keepalived/keepalived.conf
```

Enable service on Master and Backup nodes.
```bash
systemctl enable --now keepalived.service
```
