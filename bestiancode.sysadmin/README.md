# Ansible Collection for FreeBSD and Debian (Ubuntu)

This Ansible collection provides a set of roles designed for configuring and managing FreeBSD and Debian (Ubuntu) servers. While the primary focus is on Debian (Ubuntu), these roles may not be applicable to other Linux distributions.

## Installation

You can install this collection using the `ansible-galaxy` command:

```bash
ansible-galaxy collection install bestiancode.sysadmin
```

Alternatively, you can create a `requirements.yml` file and use it to install all collections and roles at once:

```bash
ansible-galaxy collection install -r requirements.yml --force
ansible-galaxy role install -r requirements.yml --force
```

Here's a sample `requirements.yml` file:

```yaml
collections:
  - name: bestiancode.sysadmin

roles:
  - name: geerlingguy.docker
  - name: newrelic.newrelic_install
```

## Usage

**Before using these roles, make sure to look at the default variables!**

Here's a sample `inventory`:

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

And a sample `playbook`:

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
    # Add other roles here

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
    # Add other roles here

...
 - other constructions can be here
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
    # Add other roles here
```
