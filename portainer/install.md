Install Docker.
```bash
apt install docker.io
```

Configure Docker Swarm.
```bash
docker swarm init
```

Install Portainer.
```bash
docker run -d -p 9000:9000 -p 8000:8000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer:latest
```
