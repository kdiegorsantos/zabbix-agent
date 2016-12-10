**[Technical overview](#technical-overview)** |
**[Prerequisites](#prerequisites)** |
**[Installation](#installation)** |
**[Running](#running)** |
**[Configuration](#configuration)** |
**[License](#license)**

# [zabbix-agent](https://github.com/kdiegorsantos/zabbix-agent)

This ansible role install and configure zabbix-agent on Red Hat Enterprise Linux and Oracle Solaris servers.

The process happens in five phases.

- Install zabbix-agent and dependencies via yum package manager on Red Hat Enterprise Linux
- Deploy the zabbix-agent binary to Oracle Solaris servers
- Configure zabbix-agent parameters
- Start and configure zabbix-agent init services
- Add or update the zabbix-agent host on the zabbix-server via zabbix-api

----

## Prerequisites

- ansible 1.4 or higher
- zabbix-api

You'll need to install zabbix-api to be able to add or update host information on zabbix-server.

```bash
pip install zabbix-api
```

Validate access to zabbix server using zabbix-api on python prompt.

```python
>>> from zabbix_api import ZabbixAPI
>>> zapi = ZabbixAPI(server="https://server/")
>>> zapi.login("login", "password")
>>> zapi.trigger.get({"expandExpression": "extend", "triggerids": range(0, 100)})
```

See also:
- http://www.zabbix.com/wiki/doc/api
- https://www.zabbix.com/documentation/3.0/manual/api
- http://www.zabbix.com/forum/showthread.php?t=15218

----

## Installation

Install using ansible-galaxy.

```bash
ansible-galaxy install kdiegorsantos.zabbix-agent
```

----

## Running

Run this role using the ansible-playbook command.

```bash
# ansible-playbook /etc/ansible/roles/zabbix-agent/role.yml
```


## Configuration

- Variables

All variables are set in default/main.yml.

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

----

## Running

Example Playbook
----------------

Run this role using the ansible-playbook command.

```bash
ansible-playbook /etc/ansible/roles/zabbix-agent/role.yml
```

----

## License

This project is licensed under the MIT license. See included LICENSE.md.
