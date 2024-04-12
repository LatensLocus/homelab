#### Agent Installation

Download packages.
```bash
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bubuntu20.04_all.deb
```

Extract packages.
```bash
dpkg -i zabbix-release_6.0-4+ubuntu20.04_all.deb
```

Install Agent.
```bash
apt update && apt install zabbix-agent
```

Open configuration file.
```bash
nano /etc/zabbix/zabbix_agentd.conf
```

Modify below values to zabbix_agentd.conf
```bash
Server=192.168.10.10
ServerActive=192.168.10.10
```

Add below values to  zabbix_agentd.conf on Proxmox LXC.
```bash
UserParameter=ct.memory.size[*],free -b | awk '$ 1 == "Mem:" {total=$ 2; used=($ 3+$ 5); pused=(($ 3+$ 5)*100/$ 2); free=$ 4; pfree=($ 4*100/$ 2); shared=$ 5; buffers=$ 6; cached=$ 6; available=$ 7; pavailable=($ 7*100/$ 2); if("$1" == "") {printf("%.0f", total )} else {printf("%.0f", $1 "" )} }'
UserParameter=ct.swap.size[*],free -b | awk '$ 1 == "Swap:" {total=$ 2; used=$ 3; free=$ 4; pfree=($ 4*100/$ 2); pused=($ 3*100/$ 2); if("$1" == "") {printf("%.0f", free )} else {printf("%.0f", $1 "" )} }'

UserParameter=ct.cpu.load[*],uptime | awk -F'[, ]+' '{avg1=$(NF-2); avg5=$(NF-1); avg15=$(NF)}{print $2/'$(nproc)'}'

UserParameter=ct.uptime,cut -d"." -f1 /proc/uptime
```

Enable and start the service.
```bash
systemctl restart zabbix-agent && systemctl enable zabbix-agent && systemctl status zabbix-agent
```

Test for LXC.
```bash
zabbix_get -s <container_ip> -k ct.memory.size
```

#### CPU Temp PVE

Edit/create the file userparameter_cputemp.conf
```bash
nano /etc/zabbix/zabbix_agentd.d/userparameter_cputemp.conf
```

Add below lines to the file.
```bash
UserParameter=basicCPUTemp.min,sensors | grep Core | awk -F'[:+°]' '{if(min==""){min=$3}; if($3<min) {min=$3};} END {print min}'
UserParameter=basicCPUTemp.max,sensors | grep Core | awk -F'[:+°]' '{if(max==""){max=$3}; if(max<$3) {max=$3};} END {print max}'
UserParameter=basicCPUTemp.avg,sensors | grep Core | awk -F'[:+°]' '{avg+=$3}END{print avg/NR}'
```
