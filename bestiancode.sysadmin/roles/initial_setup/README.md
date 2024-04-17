# Role Description

This Ansible role is specifically crafted to set up a newly configured VM or server. It performs several key tasks including the creation of essential directories, installation of necessary packages, and execution of the initial configuration.

Also this role conducts a full system upgrade. This is triggered when the flag file located at `/var/spool/initial.reboot.done` is not found.

To ensure the system is fully updated and configured before any other tasks are performed, it is recommended to execute this role as the first step in a playbook.

The creation of the flag file `/var/spool/initial.reboot.done` is handled by the `initial_reboot` role.

## Default Variables

For more information on default variables, please refer to the `defaults/main.yml` file.
