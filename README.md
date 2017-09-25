# Ansible Network Parsers


This repository contains CLI parsers using the [``parse_cli``|http://docs.ansible.com/ansible/latest/playbooks_filters.html#network-cli-filters] Ansible filter. The network IOS covered are:

* Cisco IOS
* Cisco NXOS
* Cisco IOS-XR
* Arista


The structure of the repository is as follows:

parsers
├── eos
├── ios
├── iosxr
└── nxos

In each Network OS directory one can find parsers for

* Interface details
* VLAN details
* BGP details
* OSPF details
* SYSLOG Details
* NTP Details

A number of these parsers are used the network specific fact collection modules like
`` nxos_facts `` or ``ios_facts``.

## USAGE

Here is an example of how to use a NxOS CLI parser

```
- hosts: localhost
  connection: local
  tasks:
    - name: get show interface
      nxos_command:
        commands:
            - show interface
      register: iface_output
    - name: generate fact from interface output
      set_facts:
        nxos_ifaces: "{{ iface_output.stdout[0] |parse_cli('./parsers/nxos/interfaces_parser.yml')
```

## LICENSE

MIT


## Authors

Ansible Community
