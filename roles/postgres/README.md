Role Name
=========

PostgreSQL running as docker container

Requirements
------------

N/A

Role Variables
--------------

`postgres_docker_tag`: Docker tag found at https://hub.docker.com/_/postgres

`postgres_docker_network`: Dictionary of Docker networks following https://docs.ansible.com/ansible/latest/modules/docker_container_module.html. Leave empty `[]` to not use it

`postgres_docker_exposed_port`: (default: 5432)

`postgres_docker_data_dir`: (default: /etc/postgres)

`postgres_docker_user`: (default: postgres) This variable will create the specified user with superuser power.

`postgres_docker_password`: (default: mysecretpassword) Sets the superuser password for PostgreSQL

`postgres_docker_database`: (default: mydb) Default database that is created when the image is first started

Create a read and a write user for the database
`pg_write_user`: (default: pgwrite)
`pg_write_password`: (default: mysecretpassword2)
`pg_read_user`: (default: pgread)
`pg_read_password`: (default: mysecretpassword3)

Dependencies
------------

Docker engine running on the machine

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
    - role: postgres
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
