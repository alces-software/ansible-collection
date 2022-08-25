# Overview
The `network` role allows users to configure network on the target machine using network scripts. This role can currently configure:

- Ethernet interfaces
- Bridge interfaces
- Bonded interfaces
- VLAN interfaces

The `network_connections` variable is an array of dictionaries that use the following options:
### `name` (required)
The name of the device to be configured. If configuring an `ethernet` or `vlan` interface, this must match the name of the interface. For a `bridge` or `bond`, this determines the name of the new device.

### `type` (required)
The following types are currently supported:

- ethernet
- bridge
- bond
- vlan

### `bridge` (optional)
Attach the connection to a network bridge. The bridge must also be defined as a separate device. Not supported for the `bridge` connection type.

### `interfaces` (optional)
The interfaces to use when creating a network `bond`. Not supported for any other network type.

### `ipv4` (optional)
A dictionary to configure ipv4 networking using the following options:

#### `ipv4.address` (optional)
Configure the device with a static IP address. Mutually exclusive with the `dhcp` option.

#### `ipv4.netmask` (optional)
The netmask to use alongside a static IP. Required if using the `address` option.

#### `ipv4.dhcp` (optional)
Whether to enable dhcp on the device. Mutually exclusive with the `address` option.

#### `ipv4.gateway` (optional)
Specify a default gateway. This should only be specified once on your external network connection.

#### `ipv4.dns` (optional)
Specify a dns server to use.  This should also be specified only once.

## Playbook Usage
Install the collection using Ansible Galaxy and import the role into your playbooks.
```
---
- hosts: myhosts
  tasks:
  - import_role:
      name: alces.hpc.network
    vars:
      network_connections:
          - name: eth0
            type: ethernet
            ipv4:
              dhcp: yes
```

## Network Examples
#### Configure `eth0` to use dhcp.
```
network_connections:
  - name: eth0
    type: ethernet
    ipv4:
      dhcp: yes
``` 

#### Setup static networking on `eth1`
```
network_connections:
  - name: eth1
    type: ethernet
    ipv4:
      address: 192.168.0.10
      netmask: 255.255.255.0
      gateway: 192.168.0.1
      dns: 8.8.8.8
```

#### Create a network bridge `br0` and attach interface `eth2`
```
network_connections:
  - name: br0
    type: bridge
    ipv4:
      dhcp: yes
  - name: eth2
    type: ethernet
    bridge: br0
```

#### Create a network bond `bond0` using `eth3` and `eth4`
```
network_connections:
  - name: bond0
    type: bond
    ipv4:
      address: 10.10.100.1
      netmask: 255.255.0.0
    interfaces:
      - eth3
      - eth4
```

#### Attach a network bond to a network bridge
```
network_connections:
  - name: bond0
    type: bond
    bridge: br0
    interfaces:
      - eth5
      - enp6
```
