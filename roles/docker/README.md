Role Name
=========

An Ansible role that installs the latest version of Docker CE on Ubuntu based on the official installation instructions.

Requirements
------------

N/A

Role Variables
--------------

`docker_users`: (default: root) a list of users to add to the docker group.

Dependencies
------------

N/A

Example Playbook
----------------

```yaml
- hosts: all
  become: true
  pre_tasks:
    - name: Update apt cache.
      apt:
        update_cache: true
        cache_valid_time: 600
      changed_when: false
  roles:
    - role: docker
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
