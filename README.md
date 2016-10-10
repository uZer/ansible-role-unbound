ansible-role-unbound
=====================

A brief description of the role goes here.

Requirements
------------

None

Role Variables
--------------

| Variable | Description | Default |
|----------|-------------|---------|
| unbound\_user | user of unbound | {{ \_\_unbound\_user }} |
| unbound\_group | group of unbound | {{ \_\_unbound\_group }} |
| unbound\_service | service name | unbound |
| unbound\_conf\_dir | path to dir of config directory | {{ \_\_unbound\_conf\_dir }} |
| unbound\_conf\_file | path to `unbound.conf(5)` | {{ \_\_unbound\_conf\_dir }}/unbound.conf |
| unbound\_flags | start up flags | "" |
| unbound\_config\_interface | `interface` to listen on | [] |
| unbound\_config\_outgoing\_interface | `outgoing-interface` | "" |
| unbound\_config\_do\_not\_query\_localhost | `do-not-query-localhost` | yes |
| unbound\_config\_do\_ip4 | `do-ip4` | yes |
| unbound\_config\_do\_ip6 | `do-ip6` | no |
| unbound\_config\_access\_control | `access-control` | [] |
| unbound\_config\_hide\_identity | `hide-identity` | yes |
| unbound\_config\_hide\_version | `hide-version` | yes |
| unbound\_config\_use\_syslog | `use-syslog` | yes |
| unbound\_config\_private\_address | `private-address` | ["10.0.0.0/8", "172.16.0.0/12", "192.168.0.0/16", "192.254.0.0/16", "fd00::/8", "fe80::/10"] |
| unbound\_config\_private\_domain | `private-domain` | [] |
| unbound\_config\_remote\_control\_control\_enable | `control-enable` | yes |
| unbound\_config\_remote\_control\_control\_use\_cert | `control-use-cert` | no |
| unbound\_config\_remote\_control\_control\_interface | `control-interface` | "" |
| unbound\_forward\_zone | `forward-zone` | [] |

## FreeBSD

| Variable | Default |
|----------|---------|
| \_\_unbound\_user | unbound |
| \_\_unbound\_group | unbound |
| \_\_unbound\_conf\_dir | /usr/local/etc/unbound |

## OpenBSD

| Variable | Default |
|----------|---------|
| \_\_unbound\_user | \_unbound |
| \_\_unbound\_group | \_unbound |
| \_\_unbound\_conf\_dir | /var/unbound/etc |

Created by [yaml2readme.rb](https://gist.github.com/trombik/b2df709657c08d845b1d3b3916e592d3)

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: localhost
  roles:
    - ansible-role-unbound
  vars:
    unbound_config_interface:
      - "{{ ansible_default_ipv4.address }}"
    unbound_config_outgoing_interface: "{{ ansible_default_ipv4.address }}"
    unbound_config_access_control:
      - 0.0.0.0/0 refuse
      - 127.0.0.0/8 allow
      - 10.100.1.0/24 allow
    unbound_config_private_domain:
      - example.com
    unbound_config_remote_control_control_interface: /var/run/unbound.sock
    unbound_forward_zone:
      -
        name: example.com
        forward_addr:
          - 8.8.8.8
```

License
-------

Copyright (c) 2016 Tomoyuki Sakurai <tomoyukis@reallyenglish.com>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

Author Information
------------------

Tomoyuki Sakurai <tomoyukis@reallyenglish.com>

This README was created by [ansible-role-init](https://gist.github.com/trombik/d01e280f02c78618429e334d8e4995c0)
