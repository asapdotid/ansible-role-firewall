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

| Name                        | Default Value | Description     |
| --------------------------- | ------------- | --------------- |
| `firewalld_default_zone`    | `public`      | Default zone.   |
| `firewalld_zone_interfaces` | `[]`          | Zone interface. |
| `firewalld_zone_source`     | `[]`          | Zone source.    |
| `firewalld_service_rules`   | `[]`          | Services rules. |
| `firewalld_port_rules`      | `[]`          | Port rules.     |
| `firewalld_rich_rules`      | `[]`          | Rich rules.     |

`ufw` specific variables:

| Name          | Default Value | Description            |
| ------------- | ------------- | ---------------------- |
| `ufw_logging` | `off`         | UFW logging on or off. |
| `ufw_rules`   | `[]`          | UFW Roles.             |

## License

MIT / BSD
