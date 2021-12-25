ansible-role-users
====

Manage OS groups and users (including ssh keys, authorized_keys, ssh known hosts).

Requirements
------------

* RHEL8+

Role Variables
--------------

* `users_groups_present` - list of groups to create, example:

```yaml
users_groups_present:
  - name: testgroup
```

* `users_groups_absent` - list of groups to remove, exmaple:

```yaml
users_groups_absent:
  - name: testgroup
```

* `users_present` - list of users to create (including ssh keys, authorized_keys, ssh known hosts), example:

```yaml
users_present:
  - name: myuser
    home: /mnt/myuser # optional
    authorized_keys:
      - "ssh-rsa some-key1"
      - "ssh-rsa some-key2"
    ssh_keys:
      - src: /tmp/id_rsa
        dest_file: id_rsa
      - src: /tmp/id_rsa.pub
        dest_file: id_rsa.pub
    known_hosts:
      - name: github.com
        key: "github.com ssh-rsa some-key"
        path: /mnt/myuser/.ssh/known_hosts
```

Dependencies
------------

Collections:

* `ansible.builtin`
* `ansible.posix`

Example Playbook
----------------

```
- hosts: my_servers
  vars:
    users_present:
      - name: root
        home: /root
        authorized_keys:
          - "ssh-rsa my-key"
  roles:
    - ansible-role-users
```

License
-------

GPLv3

Author Information
------------------

Vladimir Vasilev (@vladi-k)
