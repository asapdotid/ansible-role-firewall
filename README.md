<p align="center"> <img src="https://user-images.githubusercontent.com/34257858/129839002-15e3f2c7-3f75-46d4-afae-0fd207d7fdde.png" width="100" height="100"></p>

<h1 align="center">
    Ansible Role Firewall
</h1>

<p align="center" style="font-size: 1.2rem;">
    This role will install and configure the firewall. It supports `ufw`, `firewalld`.

    For Ubuntu firewall service `UFW` and RHEL/CentOS 7 or later, the `firewalld` module is used to configure the firewall.

</p>

<p align="center">

<a href="https://www.ansible.com">
  <img src="https://img.shields.io/badge/Ansible-2.10-green?style=flat&logo=ansible" alt="Ansible">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="Licence">
</a>
<a href="https://ubuntu.com/">
  <img src="https://img.shields.io/badge/ubuntu-20.x-orange?style=flat&logo=ubuntu" alt="Distribution">
</a>
<a href="https://www.centos.org/">
  <img src="https://img.shields.io/badge/CentOS-8-green?style=flat&logo=centos" alt="Distribution">
</a>

## Dependencies

- `ansible.posix.firewalld` collection
- `community.general.ufw` Collection

## Role Variables

These variables apply to all firewall types:

`firewalld` specific variables:

| Name                          | Default Value | Description                                                                                                                                                                             |
| ----------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `firewalld_default_zone`      | `public`      | Default zone.                                                                                                                                                                           |
| `firewalld_zone_interfaces`   | `[]`          | Zone interface.                                                                                                                                                                         |
| `firewalld_allowed_tcp_ports` | `['22']`      | List of allowed TCP ports.                                                                                                                                                              |
| `firewalld_allowed_udp_ports` | `['161']`     | List of allowed UDP ports.                                                                                                                                                              |
| `firewalld_nat_rules`         | `[]`          | Specify a source IP and destination port instead of opening the port globally. Optionally allow it only if it is new. With `firewalld`, this creates rich rules to the specified zone.. |
| `firewalld_rich_rules`        | `[]`          | List of ports and their protocols to NAT. With firewalld, adds rich rules to the specified zone.                                                                                        |
| `firewalld_rules`             | `[]`          | List of rules to pass to the firewalld module. Each module argument is optional.                                                                                                        |

`ufw` specific variables:

| Name          | Default Value | Description            |
| ------------- | ------------- | ---------------------- |
| `ufw_logging` | `off`         | UFW logging on or off. |
| `ufw_rules`   | `[]`          | UFW Roles.             |

## Example

```yaml
- hosts: all
  roles:
    - role: asapdotid.firewall
```

Variables pace in `vars/main.yml` on your project

### Firewalld

```yaml
firewall_allowed_tcp_ports:
  - 22
  - 80
  - 443

firewall_allowed_udp_ports:
  - 123
  - 67

firewall_nat_rules:
  - protocol: tcp
    original_port: 4022
    translated_port: 22

firewall_rich_rules:
  - source: "10.0.1.17"
    protocol: "tcp"
    dest_port: 22
    new: true
  - source: "192.168.0.0/24"
    protocol: "tcp"
    dest_port: 22

firewalld_rules:
  - service: "ssh"
    immediate: "yes"
    zone: "public"
```

### UFW

```yaml
ufw_logging: 'off'

ufw_rules:
  - rule: 'allow',
    to_port: 'ssh',
    proto: 'tcp',
    comment: 'allow incoming connection on standard ssh port'
```

## License

MIT / BSD
