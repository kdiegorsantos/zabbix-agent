zabbix-agent - Install and configure zabbix-agent
============

This ansible role can be used to install and configure zabbix-agent on RHEL 5/6/7 and Solaris 10 servers.
We have tasks to:

1. install zabbix-agent and dependencies via YUM on RHEL servers.
2. Deploy the zabbix-agent binary to Solaris servers.
3. Configure zabbix-agent parameters.
3. Start and manage zabbix-agent service.
4. Add or update the zabbix-agent host on the zabbix-server via API.

Requirements
------------
Ansible 1.5.4 or higher.


Role Variables
--------------

All variables are set in default\main.yml.

```yaml
# zabbix-api
zabbix_api_use: True                                # True or False, to enable or not zabbix-api.
zabbix_url: "http://zabbix.mydomain/zabbix"         # The main page of your zabbix server.
zabbix_api_user: "zabbix_admin_username"            # zabbix admin username.
zabbix_api_pass: "zabbix_admin_password"            # zabbix admin password.
zabbix_create_hostgroup: absent                     # if the group not exists create it or not.
zabbix_create_host: present                         # if the host not exists create it or not.
zabbix_host_status: enabled                         # enalbe or disable the host.
zabbix_useuip: 1                                    # use ip and not dns.
zabbix_host_groups_rhel:                            # default group for Linux hosts.
  - Linux Servers
zabbix_link_templates_rhel:                         # default template for Linux hosts.
  - Template OS Linux
zabbix_host_groups_sun:                             # default group for Solaris hosts.
  - Solaris Servers
zabbix_link_templates_sun:                          # default template for Solaris hosts.
  - Template OS Solaris
```



Dependencies
------------

You'll need to install zabbix-api to be able to add or update host information on zabbix-server.

Installation:
```sh
# pip install zabbix-api
```

Short example:

```python
>>> from zabbix_api import ZabbixAPI
>>> zapi = ZabbixAPI(server="https://server/")
>>> zapi.login("login", "password")
>>> zapi.trigger.get({"expandExpression": "extend", "triggerids": range(0, 100)})
```

See also:
* http://www.zabbix.com/wiki/doc/api
* https://www.zabbix.com/documentation/3.0/manual/api
* http://www.zabbix.com/forum/showthread.php?t=15218


Installation
------------

Install using ansible-galaxy.

```sh
$ ansible-galaxy install kdiegorsantos.zabbix-agent
```

Example Playbook
----------------

After change the default variables you can run this role using the ansible-playbook command.

```sh
# ansible-playbook /etc/ansible/roles/zabbix-agent/role.yml
```

License
-------

This project is licensed under the MIT license. See included LICENSE.md.


Author Information
-------

* Diego R. Santos
* [github.com](https://github.com/kdiegorsantos)


