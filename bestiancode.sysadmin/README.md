# Ansible Collection for FreeBSD and Debian(Ubuntu)

This collection provides a set of Ansible roles designed for configuring and managing Linux servers. While the primary focus is on Debian(Ubuntu) distribution, these roles may not be applicable to other Linux distributions.

In addition to Linux, these roles are being adapted to manage FreeBSD servers, because I still use FreeBSD and there are not so much roles for it in the world.

## Installation

* To install the collection, you can use the `ansible-galaxy` command:

```bash
ansible-galaxy collection install bestiancode.sysadmin
```

* Also requirements file for all list of collections can be created and used for installng all collections and roles at once:

```bash
ansible-galaxy collection install -r requirements.yml --force
ansible-galaxy role install -r requirements.yml --force
```

* Sample `requirements.yml` file:

```yaml
---

collections:
  - name: bestiancode.sysadmin

roles:
  - name: geerlingguy.docker
  - name: newrelic.newrelic_install
```

## Samples

* **First, look at default variables in roles!**

* Sample `inventory`:

```ini
managerName: admin
managerGroup: admin
managerGID: 1001
managerUID: 1001

manager_ssh_keys: |
  ssh-rsa AAAAB... manager@rsa.host
  ssh-ed25519 AAAAC... manager@ed.host

root_ssh_keys: |
  ssh-rsa AAAAB... root@rsa.host
  ssh-ed25519 AAAAC... root@ed.host
```

* Sample `playbook`:

```yaml
- hosts:
    - all
  become: true
  tags:
    - basic
    - init
  roles:
    # If collections are not defined here, it is mandatory to specify prefix bestiancode.sysadmin!
    - bestiancode.sysadmin.initial_setup

- hosts:
    - all
  become: true
  tags:
    - auth
    - init
  collections:
    # If collections are defined here...
    - bestiancode.sysadmin
  roles:
    # If you defined collections, prefix bestiancode.sysadmin is not needed.
    - auth_ssh_manager
...
 - other roles here
...

- hosts:
    - all
  become: true
  tags:
    - reboot
    - basic
    - init
  collections:
    - bestiancode.sysadmin
  roles:
    - initial_reboot
```
