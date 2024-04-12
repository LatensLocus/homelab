Update OS
```bash
sudo apt update && apt upgrade -y && reboot
```

Install prerequisites
```bash
sudo apt install git curl -y
```
Add nodejs software repository
```bash
curl -sL https://deb.nodesource.com/setup_current.x | sudo bash -
```
Install nodejs
```bash
sudo apt install nodejs -y
```
Clone from git
```bash
git clone https://github.com/louislam/uptime-kuma.git ./uptime-kuma
```
Change directory
```bash
cd uptime-kuma
```
Run setup
```bash
npm run setup
```
Run uptime-kuma
```bash
node server/server.js
```
Test on browser
```bash
http://<ipaddress:3001
```
Install PM2 if you don't have it: 
```bash
npm install pm2 -g && pm2 install pm2-logrotate
```
Start Server
```bash
pm2 start server/server.js --name uptime-kuma
```
If you want to add it to startup
```bash
pm2 save && pm2 startup
```
