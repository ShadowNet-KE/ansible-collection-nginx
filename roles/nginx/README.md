# [nginx](#nginx)

Ansible role for NGINX

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-nginx/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-nginx/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-nginx/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-nginx)|[![quality](https://img.shields.io/ansible/quality/54561)](https://galaxy.ansible.com/buluma/nginx)|[![downloads](https://img.shields.io/ansible/role/d/54561)](https://galaxy.ansible.com/buluma/nginx)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-nginx.svg)](https://github.com/buluma/ansible-role-nginx/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-nginx.svg)](https://github.com/buluma/ansible-role-nginx/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-nginx.svg)](https://github.com/buluma/ansible-role-nginx/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  pre_tasks:
    - name: Set repo if Alpine
      ansible.builtin.set_fact:
        version: "=1.21.5-r1"
      when: ansible_facts['os_family'] == "Alpine"
    - name: Set repo if Debian
      ansible.builtin.set_fact:
        version: "=1.21.5-1~{{ ansible_facts['distribution_release'] }}"
      when: ansible_facts['os_family'] == "Debian"
    - name: Set repo if Red Hat
      ansible.builtin.set_fact:
        version: "-1.21.5-1.{{ (ansible_facts['distribution'] == 'Amazon') | ternary('amzn2', ('el' + ansible_facts['distribution_major_version'] | string)) }}.ngx"
      when: ansible_facts['os_family'] == "RedHat"
  tasks:
    - name: Install NGINX
      ansible.builtin.include_role:
        name: buluma.nginx_core.nginx
      vars:
        nginx_version: "{{ version }}"
        nginx_service_modify: true
        nginx_service_timeout: 95
        nginx_logrotate_conf_enable: true
        nginx_logrotate_conf:
          paths:
            - /var/log/nginx/*.log
          options:
            - daily
            - missingok
            - rotate 14
            - compress
            - delaycompress
            - notifempty
            - sharedscripts
```



## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-nginx/blob/main/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-nginx/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|alpine|all|
|amazon|all|
|debian|buster, bullseye|
|el|7, 8|
|ubuntu|bionic, focal, jammy|
|opensuse|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-nginx/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-nginx/blob/master/CHANGELOG.md)

## [License](#license)

Apache License, Version 2.0

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)
