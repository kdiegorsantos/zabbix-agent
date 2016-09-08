zabbix-agent
============

This ansible role can be used to install and configure zabbix-agent on RHEL and Solaris servers and populate zabbix-server using zabbix-host.

Requirements
------------
RHEL 5/6 or Solaris 10.


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



Example Playbook
----------------

After change the default variables you can run this role using the ansible-playbook command.

```sh
# ansible-playbook /etc/ansible/roles/zabbix-agent/role.yml
```

License
-------

BSD


Author Information
-------

* Diego R. Santos
* [github.com](https://github.com/kdiegorsantos)


