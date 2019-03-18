# Vermilion Tech's Ansible Repository

- [Installing ansible](#installing-ansible)

### Installing Ansible for use locally
Using `pip`
```bash
pip install ansible
```

We recommend disabling host key checking
`https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html#host-key-checking`

We also recommend setting up a default user to connect with ansible

```bash
$ vim ~/.ansible.cfg
...
[defaults]
remote_user = root
private_key_file = ~/.ssh/kaden@vermilion.tech.id_rsa
...
```

### Ansible Role Descriptions

`vermilion-tech.ubuntu-base`
- Upgrades Packages
- Installs `python-pip`
- Installs python packages `docker` and `docker-compose`
- Uses `apt` `autoremove` and `autoclean`

### Playbooks Descriptions

`playbooks/ubuntu-base`
- Includes the `vermilion-tech.ubuntu-base` role
- Includes the `geerlingguy.docker` role
- Bootstraps the target with Python2 minimal by including `bootstrap-ubuntu.yml`

`bootstrap-ubuntu.yml`
There may be some cases where Python isn't already installed on the server/target machine. We provide a playbook to bootstrap the machine.

- Installs Python2 minimal on Ubuntu targets

### Examples

Use playbook `ubuntu-base` on a single host target using a custom ssh username/private_key_file
```bash
$ ansible-playbook -i elk.vermilion.tech, ubuntu-base.yml -u knelson --key-file=~/.ssh/kaden@vermilion.tech.id_rsa
```

Use playbook `ubuntu-base` on DigitalOcean droplets tagged `ubuntu-base`
```bash
$ ansible-playbook -i digital_ocean.py -l ubuntu-base ubuntu-base.yml
```

### References
- https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html
- https://docs.ansible.com/ansible/latest/user_guide/command_line_tools.html
- https://github.com/geerlingguy/ansible-for-devops/tree/master/dynamic-inventory/digitalocean
