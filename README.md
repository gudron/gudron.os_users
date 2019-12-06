gudron.os_users
=========

Meta-role for manage operation system users/groups. users, users shells.

Role Variables
--------------

### General variables

  * `users_list_params: list`
    List of users parameters. Like `name`, `shell`, `password` and etc.

    Supported parameters: [defaults/main.yml](defaults/main.yml).

    This values passed *as is* to `gudron.os_users_manager` role. 
    
    For getting more information about user variables check [gudron.os_users_manager](https://github.com/gudron/gudron.os_users_manager/blob/master/README.md) role documentation.

  * `groups_list_params: list`
    List of groups parameters.

    Supported parameters: [defaults/main.yml](defaults/main.yml).


Dependencies
------------

  * gudron.os_users_manager - [Role for manage operation system users and groups](https://github.com/gudron/gudron.os_users_manager)
  * gudron.shells - [Roles for install shells](https://github.com/gudron/gudron.shells)
  * gudron.shells_preparer - [Role for preprare user shell environment](https://github.com/gudron/gudron.shells_preparer)
  * gudron.sudo - [Role for install sudo package and manage sudo privelegies](https://github.com/gudron/gudron.sudo)

Example Playbook
----------------

    - hosts: example_project:&example_project_stage
      any_errors_fatal: "{{ any_errors_fatal | default(true) }}"
      gather_facts: True

      roles:
        - name: gudron.os_users
          vars: 
            users_list_params:
              - name: ansible_example
                is_sudo: yes
                no_pwd_sudo: false
                shell: /bin/dash
                password: somepassword
                email: example@example.com
                groups:
                  - sudo
                  - example_group2
                ssh:
                  keys:
                    - priv: /path/to/existen/ssh/key/ansible_example.pem
                      pub: /path/to/existen/ssh/key/ansible_example.pem.pub
                      comment: ansible_example
            groups_list_params:
              - name: example_group1
              - name: example_group2

License
-------

Apache
