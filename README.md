# docker-ansible-test

```bash
docker-compose up -d
docker exec -it ansible /bin/bash
```
Password: `root`

```bash
echo '
[linux]

server1
server2
server3
' | tee  /etc/ansible/hosts

ansible-config init --disabled > /etc/ansible/ansible.cfg

sed -i '/host_key_checking/c\host_key_checking=False' /etc/ansible/ansible.cfg
```

Now you can run Ansible:
```bash
ansible linux -m ping
```
