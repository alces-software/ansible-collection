# Overview
The `cleanos`  role will take a newly installed host and install basic packages and services. Currently, the role does the following:

- Disables SELinux
- Removes NetworkManager and installs `network-scripts` 
- Installed typical packages such as `vim`, `git`  and `net-tools`
- Installed typical services such as `firewalld`

The `cleanos` variable is an array of options to control the behaviour of the role.
### `disable_selinux` (default: true)
Whether to disable SELinux - defaults to to true.

### `remove_nm` (default: true)
Whether to remove `NetworkManager` and install `network-scripts` - defaults to true.

### `install_packages` (default: true)
Whether to install typical packages - defaults to true.

### `install_services` (default: true)
Whether to install typical services - defaults to true.

### `packages` (optional)
The list of packages to install. Currently defaults to:

- vim
- net-tools
- git
- yum

### `services` (optional)

The list of services to install and start. Currently defaults to:

- firewalld

## Playbook Usage
Install the collection using Ansible Galaxy and import the role into your playbooks.
```
---
- hosts: myhosts
  tasks:
  - import_role:
      name: alces.hpc.cleanos
    vars:
      cleanos:
        disable_selinux: no
```
