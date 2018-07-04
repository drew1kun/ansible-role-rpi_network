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
 - Debian (Raspbian, Minibian)
   - jessie
   - stretch

**ATTENTION!**

**vault_rpi3_network_wifi_APs** var is set in *vars/main.yml*,
which is encrypted with [ansible-vault][ansible-vault-link].

Before running the role add the following to **ansible.cfg**:

    [defaults]
    vault_password_file = .vault.key

Role Variables
--------------
| Variables | Description | Default|
|-----------|-------------|--------|
| **rpi3_network_LAN** | Wired LAN interface | `eth0` |
| **rpi3_network_WLAN** | Wireless LAN interface | `wlan0` |
| **rpi3_network_LAN_ip** | LAN interface Static IP address | `192.168.2.2` |
| **rpi3_network_LAN_netmask** | LAN interface subnet mask | `255.255.255.0` |
| **rpi3_network_LAN_gw** | Default Gateway IP address for LAN interface | `192.168.2.1` |
| **rpi3_network_wireless** | Configure wireless connections using wpa_supplicant | `yes` |
| **rpi3_network_wpa_supplicant_conf** | Path to wpa_supplicant configuration file | `/etc/wpa_supplicant/wpa_supplicant.conf` |
| **rpi3_network_wifi_APs** | List of wireless Access Points to be configured in wpa_supplicant | see [`defaults/main.yml`](defaults/main.yml) |

Dependencies
------------

None

Example Playboouk
----------------

    - hosts: rpi_3
      gather_facts: yes
      roles:
         - { role: drew_kun.rpi3_network, rpi3_network_LAN_ip: 10.0.0.1, rpi3_network_LAN: 10.0.0.254 }

License
-------

[MIT][mit-link]

Author Information
------------------

Andrew Shagayev | [e-mail](mailto:drewshg@gmail.com)

[role-badge]: https://img.shields.io/badge/role-drew__kun.rpi3__network-green.svg
[galaxy-link]: https://galaxy.ansible.com/drew_kun/rpi3_network/
[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew_kun/ansible-rpi3_network/master/LICENSE
