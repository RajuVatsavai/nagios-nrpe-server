Nagios NRPE Server Config
=========

An Ansible role to handle the installation and rollout of the Nagios NRPE Daemon.

I've only selected certain platforms that I know this 100% works on, but it should work on any platform that NRPE can be installed on.

Currently supports:

 * Ubuntu
   - Precise
   - Trusty
 * CentOS
   - 7.2

Role Information
----------------

This role gives you the ability to deploy plugins on a global and per-server basis. This can be done by putting plugins into [`files/plugins/global`](files/plugins/global) or by creating a folder in `files/plugins/` that is the servers [FQDN](http://en.wikipedia.org/wiki/Fully_qualified_domain_name).

You can find out your servers FQDN by running the [Ansible Setup](http://docs.ansible.com/setup_module.html) module.

Role Variables
--------------

  * *nagios_nrpe_server_bind_address*: 127.0.0.1
  * *nagios_nrpe_server_port*: 5666
  * *nagios_nrpe_server_allowed_hosts*: 127.0.0.1

These are OS specific and likely wont want to be changed

Ubuntu:

  * *nagios_nrpe_server_pid*: /var/run/nagios/nrpe.pid
  * *nagios_nrpe_server_user*: nagios
  * *nagios_nrpe_server_group*: nagios
  * *nagios_nrpe_server_service*: nagios-nrpe-server
  * *nagios_nrpe_server_plugins_dir*: /usr/lib/nagios/plugins
  * *nagios_nrpe_server_dir*: /etc/nrpe.d
  * *nagios_nrpe_managed_files: ['nrpe.cfg']
  
CentOS:

  * *nagios_nrpe_server_pid*: /var/run/nrpe/nrpe.pid
  * *nagios_nrpe_server_user*: nrpe
  * *nagios_nrpe_server_group*: nrpe
  * *nagios_nrpe_server_repo_redhat*: epel
  * *nagios_nrpe_server_service*: nrpe
  * *nagios_nrpe_server_dir*: /etc/nagios
  * *nagios_nrpe_managed_files*: ['nrpe.cfg']

Dependencies
------------

RedHat based OS's must have the EPEL repo.

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - gregfaust.nagios_nrpe
   vars:
     nagios_nrpe_server_allowed_hosts:
       - 192.168.0.1
       - 127.0.0.1
     nagios_nrpe_server_bind_address: 127.0.0.1
     nagios_nrpe_server_port: 5666
```

License
-------

MIT

Author Information
------------------

Forked from Mooash [here](http://www.mooash.me)
