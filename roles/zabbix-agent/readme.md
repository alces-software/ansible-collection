This role will install zabbix and zabbix-agent, creating relevant directories, as well as the zabbix user.
It will then define the zabbix server and start the agent service.

>>You will need:<<
ansible-core
ansible-galaxy
ansible.posix

>>You will need to add:<<
Your zabbix server link

The playbook will initially install zabbix and zabbix agent respectively. Currently zabbix v6.2-1, change this if outdated.

Then it will enable zabbix-agent so that it launches on startup.

After which it, creates the zabbix user and its default directory in /etc.

It will then, create a directory for your scripts.

Next, the playbook will edit the config, to direct zabbix-agent to your zabbix server.

Finally, it will launch the service.
