# Ansible horde role

This is an [Ansible](http://www.ansible.com) role to setup the [Horde Groupware Webmail Edition](https://www.horde.org/apps/webmail).

## Requirements

This role requires a LAMP (Linux, Apache, MySQL, PHP) stack.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Usage

This is an example playbook:

```yaml
---

- hosts: all
  roles:
    - role: amtega.horde
      vars:
        horde_packages:
          - php-horde-imp
          - php-horde-ingo
          - php-horde-kronolith
          - php-horde-mnemo
          - php-horde-nag
          - php-horde-passwd
          - php-horde-turba
          - php-channel-horde
          - php-horde-content
        horde_files:
          - file: "{{ horde_config_dir }}/ingo/conf.php"
            description: "INGO configuration file"
            state: present
            content: |
              <?php
              /* CONFIG START. DO NOT CHANGE ANYTHING IN OR AFTER THIS LINE. */
              // $Hash: 250aa3932bf63e25d99fe1399ded4932870fa93f
              // $Id: 48142d13ef06c07f56427fe5b43981631bdbfdb0 $
              $conf['storage']['params']['driverconfig'] = 'horde';
              $conf['storage']['driver'] = 'sql';
              $conf['rules']['userheader'] = true;
              $conf['spam']['header'] = 'X-Spam-Level';
              $conf['spam']['char'] = '*';
              $conf['spam']['compare'] = 'string';
              /* CONFIG END. DO NOT CHANGE ANYTHING IN OR BEFORE THIS LINE. */

```

## Testing

Tests are based on [molecule with docker containers](https://molecule.readthedocs.io/en/latest/installation.html).

```shell
cd amtega.horde

molecule test --all
```

## License

Copyright (C) 2021 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- José Manuel Fandiño Pita
- Juan Antonio Valiño García
