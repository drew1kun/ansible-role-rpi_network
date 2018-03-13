Ansible role: rpi3_network
=========

[![MIT licensed][mit-badge]][mit-link]
[![Galaxy Role][role-badge]][galaxy-link]

This role does the following:

 - Configures wireless adapters (built in and external USB) to have persistent names (wlan0, wlan1 etc.) based on MAC addresses
 - Sets up wireless adapter to get IP address from DHCP
 - Sets up wired ethernet adapter to get IP address from DHCP
 - Sets up wired ethernet adapter to get additional static IP address
 - Sets up default IP route via configured default gateway

Requirements
------------

NOTE: Role requires Fact Gathering by ansible!

One of the following OS (or deriviatives):
 - Debian jessie (Raspbian, Minibian)

Role Variables
--------------
| Variables | Description | Default|
|-----------|-------------|--------|
| **rpi3_network_LAN** | Wired LAN interface | eth0 |
| **rpi3_network_WLAN** | Wireless LAN interface | wlan0 |
| **rpi3_network_LAN_ip** | LAN interface Static IP address | 192.168.2.2 |
| **rpi3_network_LAN_netmask** | LAN interface subnet mask | 255.255.255.0 |
| **rpi3_network_LAN_gw** | Default Gateway IP address for LAN interface | 192.168.2.1 |

Dependencies
------------

None

Example Playboouk
----------------

    - hosts: rpi_3
      gather_facts: yes
      roles:
         - { role: drewshg312.rpi3_network, rpi3_network_LAN_ip: 10.0.0.1, rpi3_network_LAN: 10.0.0.254 }

License
-------

[MIT][mit-link]

Author Information
------------------

Andrew Shagayev | [e-mail](mailto:drewshg@gmail.com)

[role-badge]: https://img.shields.io/badge/role-drew--kun.rpi3__network-green.svg
[galaxy-link]: https://galaxy.ansible.com/drew-kun/rpi3_network/
[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew-kun/ansible-rpi3_network/master/LICENSE
