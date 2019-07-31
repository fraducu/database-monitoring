Role Name
=========

Prometheus monitoring server running as Docker container

Requirements
------------

N/A

Role Variables
--------------

- `prometheus_docker_tag`: (default: v2.10.0)
- `prometheus_docker_exposed_port`: (default: 9090)
- `prometheus_additional_command_args`: Additional command line arguments for prometheus
- `prometheus_docker_network`: (default: [])Docker network for prometheus Docker applications
- `prometheus_static_targets`: (default: localhost:9090)
- `prometheus_targets`: Optional list of dictionaries of targets:
  - `group`: A list of Ansible groups (optional)
  - `hosts`: A list of hosts (optional)
  - `port`: The port to be monitored
  - `jobname`: The prometheus job-name
  - `scrape_interval`: Prometheus scrape interval (optional)
  - `metrics_path`: Path to metrics (optional)
- `prometheus_sd_targets`: Optional list of dictionaries of additional targets:
  - `groupname`: The name of the configuration target file, used to name a configuration file so must be unique
  - `group`: A list of Ansible groups (optional)
  - `hosts`: A list of hosts (optional)
  - `port`: The port to be monitored
  - `jobname`: The prometheus job-name


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
    - role: prometheus
    prometheus_targets:
      - hosts: [localhost]
        port: 9187
        jobname: postgres-metrics
        scrape_interval: 5s
        metrics_path: /metrics
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
