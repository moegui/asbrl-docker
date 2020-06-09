Role Name
=========

Install the last version of the Docker Community Edition.

Requirements
------------

+ Git (need it for Galaxy Role).
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

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
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
