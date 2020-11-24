Ansible role: Docker
=========

This role is child role of container_runtime and used to install and configure docker.

For now, it does the following:
- Adds docker-ce repository
- Installs docker and containerd
- Configures docker daemon to satisfy kubernetes pre-install requirements


Requirements
------------

This is not strict requirements and it may not work with other versions than tested ones.
Anyway. feel free to test by yourself, suggest addition of new functionality and contribute.

Role is tested with:
- Ansible version >= 2.8.6
- CentOS version >= 7.6 (1803)


Role Variables
--------------

Variables and their descriptions copied from defaults/main.yml

```bash

# Version of docker community edition to install:
docker_ce_version: 18.06.2.ce

# Version of containerd package to install:
docker_containerd_version: 1.2.10

```


Dependencies
------------

none


Example Playbook
----------------

```bash
---
- hosts: localhost
  gather_facts: false
  become: no
  tasks:
  - name: Check ansible version >=2.8.6
    assert:
      msg: Ansible must be v2.8.6 or higher
      that:
      - ansible_version.string is version("2.8.6", ">=")
    tags:
    - check
  vars:
    ansible_connection: local

- hosts: all
  become: yes
  tasks:
  # From parent role when "container_runtime_name: docker" is set inside your variables:
  - import_role:
      name: caermeglaeddyv.ansible_role_containr_runtime
  # Or directly:
  - import_role:
      name: caermeglaeddyv.ansible_role_docker

```

More detailed examples ( inventories, playbooks etc. ) of this and other roles can be found [here](https://github.com/caermeglaeddyv/examples/tree/dev/ansible).

It's highly recommended to start you test deploys from there, especially if you use Google Cloud Platform or VMware vCenter as your infrastructure, for now that [repository](https://github.com/caermeglaeddyv/examples) contains [Packer](https://github.com/caermeglaeddyv/examples/tree/dev/packer) and [Terraform](https://github.com/caermeglaeddyv/examples/tree/dev/terraform) examples to build templates and deploy machines on this platforms.


License
-------

[Apache 2.0](https://github.com/caermeglaeddyv/ansible-role-docker/blob/dev/LICENSE)


Author Information
------------------

Copyright 2020 [caermeglaeddyv](https://github.com/caermeglaeddyv)
