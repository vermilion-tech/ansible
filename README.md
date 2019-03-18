# Vermilion Tech's Ansible Repository

---

### Setup
1. Install Ansible

`https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html`

- We also recommend disabling host key checking
  - `https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html#host-key-checking`

- We also recommend setting up a default user to connect with ansible

  - ```bash
    $ vim ~/.ansible.cfg
    ...
    [defaults]
    remote_user = root
    private_key_file = ~/.ssh/kaden@vermilion.tech.id_rsa
    ...
    ```

2. Clone the repository

`$ git clone git@github.com:vermilion-tech/ansible.git`

3. Install Ansible Roles from Ansible Galaxy

  - `$ ansible-galaxy install -r requirements.yml`

4. Execute Master Playbook

  - `$ ansible-playbook -i digital_ocean.py playbook.yml`

### Playbooks Descriptions

- `playbook.yml`
  - Master playbook that includes both `ubuntu-base.yml` and `loadbalancers.yml` playbooks

- `ubuntu-base.yml`
  - Bootstraps the target with Python2 minimal by including `bootstrap-ubuntu.yml`
  - Includes the `kadenlnelson.ansible_role_ubuntu_base` role
  - Targets Droplets tagged `ubuntu-base`

- `loadbalancers.yml`
  - Installs Traefik as a Docker container on Droplets tagged `loadbalancers`

### References
- https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html
- https://docs.ansible.com/ansible/latest/user_guide/command_line_tools.html
- https://github.com/geerlingguy/ansible-for-devops/tree/master/dynamic-inventory/digitalocean
