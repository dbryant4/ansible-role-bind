# Bind Role

[![Build
Status](https://travis-ci.org/dbryant4/ansible-role-bind.svg?branch=master)](https://travis-ci.org/dbryant4/ansible-role-bind)

## Description

This role manages the installation of the bind DNS server on a Raspberry Pi, although it
should be able to manage any other Debian based system. When paired with the DHCP role, the bind server setup using this role will automatically create new A and PTR records for each DHCP address assigned by the DHCP server.


## Provides

1. A Bind DNS server

## Requires

1. Ansible 1.6.10 or higher
2. Raspberry Pi (possibly other Debian based systems)

## Variables

- bind_dns_forwarder - The server to pass any unresolvable DNS queries to. `8.8.8.8` is a good default.
- bind_top_level_domain - The top level domain. This is used to create a zone. For example, I use `home` for my home network which means each host is `hostname.home`.
- bind_reverse_zone - Reverse DNS zone. This is usually the subnet of your network, only with the octets reversed. For example: `0.168.192` for the 192.168.0.0/24 network.
- bind_packages - packages to install to provide the Bind dns service. This should never change.
- bind_service_name - Service name of bind. By default, `bind9` is used. This should not be changed.
- bind_static_records - Defines the static DNS records which are set
  statically.

### Changing Variable Values

To Change the value of variables, create a file in `host_vars/` or `group_vars/` or define variables in the playbook.

There are other options for changing variable values. See [Ansible
Variable
Documentation](http://docs.ansible.com/playbooks_variables.html) for
more ideas.

## Usage

Include this role in your plays and set varaibles as desired.

```yaml
---
  name: bind-servers
  hosts: bind-servers
  vars:
  	bind_dns_forwarder: '192.168.0.1'
  roles:
    - bind
```

## Tests
This role includes Travis CI tests.
