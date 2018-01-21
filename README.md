rpi3_network
=========

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

No special requirements

Role Variables
--------------

No variable settings required

Dependencies
------------

Does not depend on other roles

Example Playbook
----------------

    - hosts: rpi_3
      roles:
         - rpi3_network

License
-------

MIT

Author Information
------------------

Andrew Shagayev
