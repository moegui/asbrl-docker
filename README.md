asbrl-docker
=========

Install the latest stable version of the Docker Community Edition.

Requirements
------------

+ Git (need it for using Galaxy Role).
+ Set gather_facts on true.
+ The role is prepared to run on **Ubuntu** and **Centos** enviroments. 

Role Variables
--------------
  > Any default value can be overrided by import-task/vars
``` 
asbrl_docker_install_docker: true
asbrl_docker_install_docker_daemon: {"insecure-registries": ["10.0.0.0/8","172.16.0.0/12","192.168.0.0/16"]}

asbrl_docker_install_certificates: false
certificates_certbot_version: "latest"

asbrl_docker_install_registry: false
dockerRegistry_version: "2"

asbrl_docker_install_watchtower: false
watchtower_version: "latest"

# Used only for Debian/Ubuntu.
docker_apt_arch: amd64
docker_apt_repository: "deb [arch={{ docker_apt_arch }}] https://download.docker.com/linux/{{ ansible_distribution | lower }} {{ ansible_distribution_release }} stable"
docker_apt_ignore_key_error: true
docker_apt_gpg_key: https://download.docker.com/linux/{{ ansible_distribution | lower }}/gpg

# Used only for RedHat/CentOS/Fedora.
docker_yum_repo_url: https://download.docker.com/linux/{{ (ansible_distribution == "Fedora") | ternary("fedora","centos") }}/docker-ce.repo
docker_yum_gpg_key: https://download.docker.com/linux/centos/gpg
``` 

# custom vars
``` 
vars: 

```

Dependencies
------------

None

Example Playbook
----------------

```
- name: Deploy
  gather_facts: true
  hosts: default
  order: sorted
  become: true

  pre_tasks:

  - name: Install git (need it for Galaxy Roles)
    package:
      name : "git"
      state : present
      update_cache : yes    

  - name: Install Galaxy Roles
    local_action: command ansible-galaxy install -f -r requirements.yml --roles-path /etc/ansible/roles

  tasks:

  - name: Installing Docker CE
    include_role:
      name: asbrl-docker
    vars:
      asbrl_docker_install_docker: true
      asbrl_docker_install_certificates: false
      asbrl_docker_install_registry: false
      asbrl_docker_install_watchtower: false
```

License
-------

BSD

Author Information
------------------

www.moegui.com
