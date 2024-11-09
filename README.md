# docker-ansible-test

```bash
docker-compose up -d
docker exec -it ansible /bin/bash
```

Now you can run Ansible:
```bash
ansible linux -m ping
```
