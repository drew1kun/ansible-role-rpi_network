# Ansible role: rpi_network

[![MIT licensed][mit-badge]][mit-link]
[![Galaxy Role][role-badge]][galaxy-link]

This role does the following:

 - Configures wireless adapters (built in and external USB) to have persistent names (wlan0, wlan1 etc.) based on MAC addresses
 - Sets up wireless adapter to get IP address from DHCP
 - Sets up wired ethernet adapter to get IP address from DHCP
 - Sets up wired ethernet adapter to get additional static IP address
 - Sets up default IP route via configured default gateway

Requirements
----

**NOTE:** Role requires Fact Gathering by ansible!

One of the following distros (or derivatives) required:

 - Debian | [Raspberry Pi OS][rpi-os-link] | Raspbian | [Minibian][minibian-link]
    - jessie
    - stretch
    - bullseye

Role Variables
----
| Variables | Description | Default|
|-----------|-------------|--------|
| `rpi_network_LAN` | Wired LAN interface | `eth0` |
| `rpi_network_WLAN` | Wireless LAN interface | `wlan0` |
| `rpi_network_LAN_ip` | LAN interface Static IP address | `192.168.3.2` |
| `rpi_network_LAN_netmask` | LAN interface subnet mask | `255.255.255.0` |
| `rpi_network_LAN_gw` | Default Gateway IP address for LAN interface | `192.168.3.1` |
| `rpi_network_wireless` | Configure wireless connections using wpa_supplicant | `true` |
| `rpi_network_wpa_supplicant_conf` | Path to wpa_supplicant configuration file | `/etc/wpa_supplicant/wpa_supplicant.conf` |
| `rpi_network_wifi_APs` | List of wireless Access Points to be configured in wpa_supplicant | see [`defaults/main.yml`](defaults/main.yml#L20) |


**ATTENTION!**
If `rpi_network_wireless` is set to `true`, then
make sure you override the `vault_rpi_network_wifi_APs` var as it contains a sensitive data for your wireless networks,
such as WPA passphrase and network ESSID...

It is highly recommended to encrypt with [ansible-vault][ansible-vault-link].

Before running any playbook which uses this role, add the following to **ansible.cfg**:

```
[defaults]
vault_password_file = .vault.key
```

Dependencies
----

None

Example Playboouk
----

```yaml
- hosts: rpi_3
  gather_facts: yes

  vars_files:
  - vars/vault.yml  # Use of ansible-vault is strongly encouraged for storing sensitive info

  roles:
  - role: drew1kun.rpi_network
    rpi_network_LAN_ip: 10.0.0.1
    rpi_network_LAN_netmask: 255.255.255.0
    rpi_network_LAN_gw: 10.0.0.254
    rpi_network_wifi_APs:
    - id_str: home
      hidden: no
      essid: "{{ vault_bootstrap_core__rpi_network_wifi_APs[0].essid }}"
      passphrase: "{{ vault_bootstrap_core__rpi_network_wifi_APs[0].passphrase }}"
      priority: 10
    when: ansible_os_family == 'Debian'
```

*vars/vault.yml*:

```yaml
vault_bootstrap_core__rpi_network_wifi_APs:
# only sensitive stuff goes here:
- essid: YourSensitiveESSID
  passphrase: YourSecureWPA_Passphrase
```

License
----

[MIT][mit-link]

Author Information
----

Andrew Shagayev | [e-mail](mailto:drewshg@gmail.com)

[role-badge]: https://img.shields.io/badge/role-drew1kun.rpi__network-green.svg
[galaxy-link]: https://galaxy.ansible.com/drew1kun/rpi_network/
[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew1kun/ansible-rpi_network/master/LICENSE
[minibian-link]: https://minibianpi.wordpress.com/
[rpi-os-link]: https://www.raspberrypi.com/software/operating-systems/
