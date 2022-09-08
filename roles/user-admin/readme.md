This role can create groups and users, as well as adding authorized_keys, and giving users sudo access.

Defaults contains a generic user, edit their details, and add additional users if you wish.
It also contains a blank public key file, this is where the role will currently check for a key.

The first block creates a group from provided details, and verifies its existance.

The second block creates a user with these details, and adds them to selected groups.

The third will add a public key, if you have defined one, to their authorized_keys folder.

The final block gives the user sudo privilages, by creating a sudoers file for them.

This example playbook shows usage:

---
- hosts: localhost
  tasks:
    - name: Create users
      include_role:
        name: user-admin
