Ansible Role: Jenkins
=====================================

[![Amol Ovhal][amol_avatar]][amol_ovhal]

[Amol Ovhal][amol_ovhal] 

  [amol_ovhal]: http://www.portfolio.amolovhal.com/
  [amol_avatar]: https://gitlab.com/uploads/-/system/user/avatar/10044525/avatar.png

An Jenkins role to install and configure Jenkins server.

Features
----------------
* This role will check the system requirement(like memory and cpu cores) of remote host and if system requirements are satisfied then it will install latest jenkins version available in repository but if you want to install a specific veriosn you may pass it in variables.
* This role is configuring jenkins global credentials as a code. To use this feature you just need to set variable as **configuration_as_code="enabled"**

Supported OS
------------
  * CentOS:7
  * CentOS:6
  * Ubuntu:bionic
  * Ubuntu:xenial
  * Amazon AMI

Dependencies
------------
* Java {version 8 preferred}

Requirements
------------
* curl
* libselinux-python
* initscripts
* apt-transport-https

Directory Layout
----------------
```
amol@amol:~/github/ansible/Jenkins$ tree
.
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   ├── configuration_as_code_task.yml
│   ├── main.yml
│   ├── plugins.yml
│   ├── pre_flight_check.yml
│   ├── settings.yml
│   ├── setup-Debian.yml
│   └── setup-RedHat.yml
├── templates
│   ├── basic-security.groovy
│   └── jenkins_configuration_as_code_template.yaml.j2
└── vars
    ├── adminpass.yml
    ├── configuration_as_code_variables.yml
    ├── Debian.yml
    ├── RedHat.yml
    └── system.yml

6 directories, 18 files
```
Role Variables
--------------

|**Variables**| **Default Values**| **Description**|
|----------|---------|---------------|
| memory | 1000 | total memory(in mb) that should be present at remote host|
| core | 1 | total number of cores that should be present at remote host|
| jenkins_admin_username | admin | Username of Admin |
| jenkins_admin_password | admin | Password for Admin user|
| jenkins_connection_delay | 5 | Wait for Jenkins to start up before proceeding |
| jenkins_connection_retries | 60| Retry to execute task if it fails to start Jenkins |
| jenkins_home | /var/lib/jenkins | Home Directory of jenkins|
| jenkins_hostname | localhost| Hostname for Jenkins |
| jenkins_http_port | 8080 | Port on which Jenkins runs|
| jenkins_jar_location | /opt/jenkins-cli.jar | Location where jar file for jenkins stores|
| jenkins_url_prefix | ""| URL prefix used in jenkins url|
| jenkins_java_options | "-Djenkins.install.runSetupWizard=false" | |
| jenkins_plugins| ['git']| Plugins add in Jenkins|
| jenkins_plugins_state | present | Jenkins plugin state|
| jenkins_plugin_updates_expiration | 86400 | Number of seconds after which a new copy of the update-center.json file is downloaded|
| jenkins_plugin_timeout | 300 | Jenkins Server connection timeout in secs|
| jenkins_plugins_install_dependencies | yes | Defines whether to install plugin dependencies. |
| jenkins_process_user | jenkins | Jenkins process username|
| jenkins_process_group | "{{ jenkins_process_user }}" | Jenkins process groupname|
| configuration_as_code | "disabled"  | Update its value to "enabled" for managing global credential as a code |

Playbook Example 
----------------
```
---
- name: Jenkins setup
  hosts: server
  become: true
  roles:
    - role: Jenkins
...

$  ansible-playbook playbook.yml -i inventory

```

Inventory
----------
An inventory should look like this:-
```ini
[server]                 
192.xxx.x.xxx    ansible_user=ubuntu 
```



### Contributor :

[![Amol Ovhal][amol_avatar]][amol_homepage]<br/>[Amol Ovhal][amol_homepage] 

  [amol_homepage]: https://gitlab.com/amol.ovhal
  [amol_avatar]: https://gitlab.com/uploads/-/system/user/avatar/10044525/avatar.png
