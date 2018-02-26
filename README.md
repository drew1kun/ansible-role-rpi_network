Ansible role: rpi3_network
=========

[![MIT licensed][mit-badge]][mit-link]
[![Galaxy Role][role-badge]][galaxy-link]

This role does the following:

 - Configures built-in wireless adapter to have persistent name (wlan0);
 - Configures external wireless adapters to have presistent names starting from wlan1
 - based on MAC address
 - Sets up built-in wireless adapter to get IP address from DHCP
 - Sets up wired ethernet adapter to get IP address from DHCP
 - Sets up wired ethernet adapter to get additional static IP address 192.168.2.2
 - Sets up default IP route via 192.168.2.1

Requirements
------------

One of the following OS (or deriviatives):
 - Debian
 - Raspbian
 - Minibian

Role Variables
--------------

No variable settings required

Dependencies
------------

None

Example Playbook
----------------

    - hosts: rpi_3
      roles:
         - drewshg312.rpi3_network

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
