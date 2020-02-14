install_pkgs
=========

This is a ansible role to install packages by downloading archive or yum

Usage
-----

Copy the content below in the section [Example requirements.yml](#example-requirementsyml), and paste it as "requirements.yaml" to a playbook folder, execute `ansible-galaxy install -r requirement.yaml` to install this role

Requirements
------------

CentOS / RedHat / Amazon

Role Variables
--------------

required:
- `env_file_path`: the shell script to export "path" to $PATH
- `pkg:`
  `name`: package name, it will be used for naming directory in folder "/opt"
  `url`: the url of archive package
  `bin_path_in_pkg`: the "/bin" path in package archive
  `archive_name`: the download archive name to save
  `type`: the type of the package to install, choose in ["yum", "archive"]
- `pkg:`
  `type`: the type of the package to install, choose in ["yum", "archive"]
  `name:` a list of package name in the yum repos to install

optional:
- `installation_group`: the group of installation directory, "root" as default
- `installation_owner`: the owner of installation directory, "root" as default

Dependencies
------------

``` yaml
- src: https://github.com/Stark-X/ansible-role-add_to_path.git
  version: "1.0"
  name: add_to_path
- src: https://github.com/Stark-X/ansible-role-mandatory.git
  version: "1.0"
  name: mandatory
```

Example Playbook
----------------

``` yaml
- hosts: servers
  become: true
  tasks:
    - include_role:
        name: install_pkgs
      vars:
        pkg:
          type: yum
          name: unzip
    - include_role:
        name: install_pkgs
      loop:
        - type: archive
          name: maven
          url: http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
          archive_name: apache-maven-3.6.3-bin.tar.gz
          bin_path_in_pkg: apache-maven-3.6.3/bin
        - type: yum
          name: 
            - wget
      loop_control:
        loop_var: pkg
```

Example requirements.yml
-----------------------

``` yaml
- src: https://github.com/Stark-X/ansible-role-install_pkgs.git
  version: "1.0"
  name: install_pkgs
```

License
-------

BSD

Author Information
------------------

Author: Stark-X

Mail: xiaojiezhi2@gmail.com

Blog: https://blog.stark-x.cn
