# Ansible <!-- this role name --> role

This is an [Ansible](http://www.ansible.com) role which setup the [Horde Groupware Webmail Edition](https://www.horde.org/apps/webmail)

## Requirements

This role requires a LAMP (Linux, Apache, MySQL, PHP) stack.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Tests

<!-- A description of the tests provided by the role should go here. For example: -->

The role provides these tests:

- `thisrole_test1`: description of the test
- `thisrole_test2`: description of the test
- `thisrole_testN`: description of the test

## Dependencies

- [amtega.check_platform](https://galaxy.ansible.com/amtega/check_platform)
- [amtega.proxy_client](https://galaxy.ansible.com/amtega/proxy_client)
- [amtega.packages](https://galaxy.ansible.com/amtega/packages)
- [amtega.php](https://galaxy.ansible.com/amtega/php)
- [amtega.apache](https://galaxy.ansible.com/amtega/apache)
- [amtega.mysql](https://galaxy.ansible.com/amtega/mysql)

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
          - file: "{{ horde_config_dir }}/ingo/conf.php2"
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

Tests are based on docker containers. You can setup docker engine quickly using the playbook `files/setup.yml` available in the role [amtega.docker_engine](https://galaxy.ansible.com/amtega/docker_engine).

  Once you have docker, you can run the tests with the following commands:

```shell
$ cd amtega.horde/tests
$ ansible-playbook main.yml
```

## License

Copyright (C) 2021 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information
