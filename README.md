assert
=========

[![Build Status](https://travis-ci.org/wate/ansible-role-assert.svg?branch=master)](https://travis-ci.org/wate/ansible-role-assert)

assertモジュールを利用した検証を行いやすくします。

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Example Playbook
----------------

```yml
- hosts: servers
  tasks:
    - name: assert packages
      include_role:
        name: assert
        tasks_from: package
      vars:
        assert_package:
          name: "{{ item }}"
      loop:
        - httpd
        - mariadb-server
    - name: assert service
      include_role:
        name: assert
        tasks_from: service
      vars:
        assert_service:
          name: "{{ item }}"
      loop:
        - httpd
        - mariadb
    - name: assert port
      include_role:
        name: assert
        tasks_from: port
      vars:
        assert_port:
          port: "{{ item }}"
      loop:
        - 80
        - 3306
    - name: assert user
      include_role:
        name: assert
        tasks_from: user
      vars:
        assert_user:
          name: "{{ item }}"
      loop:
        - foo_user
        - bar_user
    - name: assert group
      include_role:
        name: assert
        tasks_from: user
      vars:
        assert_group:
          name: "{{ item }}"
      loop:
        - foo_group
        - bar_group
    - name: assert file
      include_role:
        name: assert
        tasks_from: file
      vars:
        assert_file:
          path: "{{ item.path }}"
          exists: "{{ item.exists }}"
          is_dir: "{{ item.is_dir | default(None) }}"
          is_file: "{{ item.is_file | default(None) }}"
      loop:
        - path: /opt/custom
          exists: true
          is_dir: true
        - path: /etc/custom/config.ini
          exists: true
          is_file: true
```

License
-------

MIT
