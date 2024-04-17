# Role Description

This Ansible role manages the initial reboot process for a newly configured VM or server. It operates by checking for a flag file located at `/var/spool/initial.reboot.done`.

If this file is not present, it signifies that the initial configuration has been completed, but a reboot has not yet been performed. In this scenario, the role will create the flag file and trigger a reboot to finalize the setup process.

For optimal results, this role should be executed as the final step in a playbook.
