# Overview
The `firewalld`  role allows users to configure firewalld zones on a target host. The role can currently configure:

- New zones
- Adding interfaces to zones
- Adding ports to zones


The `firewall_zones` variable is an array of dictionaries that use the following options:

### `name` (required)
The name of the firewall zone to configure. Will be created if it does not already exist.

### `interfaces` (optional)
An array of interfaces to add to this firewall zone.

### `ports` (optional)
An array of ports to allow on the firewall zone.

## Playbook Usage
Install the collection using Ansible Galaxy and import the role into your playbooks.
```
---
- hosts: myhosts
  tasks:
  - import_role:
      name: alces.hpc.firewalld
    vars:
      firewall_zones:
        - name: external
          interfaces:
            - eth0
          ports:
            - 22/tcp
            - 80/tcp
        - name: trusted
          interfaces:
            - eth1
            - eth2
```
