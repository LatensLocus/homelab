#### Installation

Add Ansible repository.
```bash
sudo apt-add-repository ppa:ansible/ansible
```

Install Ansible.
```bash
sudo apt install ansible
```

#### Setup SSH keys

Create a key pair.
```bash
ssh-keygen
```

Copy public key.
```bash
ssh-copy-id username@remote_host
```

#### Setup inventory File

Edit the inventory file.
```bash
sudo nano /etc/ansible/hosts
```

Paste and modify text below to inventory file.
```bash
[servers]
servername ansible_host=ipaddress

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

Display the list of the inventory file.
```bash
ansible-inventory --list -y
```

#### Run an adhoc update, upgrade and remove apt command

Run as privileged user.
```bash
ansible all -m apt -a "upgrade=yes update_cache=yes autoremove=yes cache_valid_time=86400" --become
```

Run as logged-on user.
```bash
ansible all -m apt -a "upgrade=yes update_cache=yes autoremove=yes cache_valid_time=86400"
```

#### Install and remove packages

Install a package.
```bash
ansible all -m apt -a "name=nginx" --become -K
```

Remove a package.
```bash
ansible all -m apt -a "name=nginx state=absent" --become  -K
```

#### Restarting servers

Run command.
```bash
ansible all -a "/sbin/reboot"  --become  -K
```

#### Restarting services

Run command.
```bash
ansible all -i inventory -m service -a "name=servicename state=restarted" --become  -K
```
