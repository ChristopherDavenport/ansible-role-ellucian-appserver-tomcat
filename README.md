# Ellucian Appserver Tomcat

[![Build Status](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-appserver-tomcat.svg?branch=master)](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-appserver-tomcat) [![Gitter](https://img.shields.io/gitter/room/ansible-role-ellucian-appserver-tomcat/Lobby.svg)](https://gitter.im/ansible-role-ellucian-appserver-tomcat/Lobby)

This is a single role to provision correctly tomcat appservers correctly for
Ellucian Banner 9 Applications.

## Role Variables

Each of these variables are required.

`ellucian_environment_name` is the environment listed in Ellucian Solutions Manager

`ellucian_tomcat_db_hostname` is the hostname of your Banner Database  

`ellucian_tomcat_db_port` is the port of the database.  

`ellucian_tomcat_db_sid` is the sid of the database.

`ellucian_tomcat_banproxy_password` and `ellucian_tomcat_banssuser_password`
are required passwords for connecting to the database.

`ellucian_tomcat_extra_libs_path` is a list of extra dependencies to add,
which should be xdb6.jar and ojdbc6.jar

`ellucian_wgetrc_http_password` is the password for access to Ellucian Solution
Manager

`ellucian_nfs_server` is the Jobsubmission Server for this environment.

`ellucian_nfs_remote_mount` is the location of the staging directory
on the Jobsubmission box.

`ellucian_jenkins_authorize_key` is the key that we are putting in Trusted Keys
to allow access for the Ellucian Solution Managers Jenkins installation to
control this box as a slave.

`ellucian_cacerts` is a list of certificates to enter into cacerts. Specifically
the names of the key, the alias, and how to get it; either local or remote.

```yaml
# ellucian_environment_name:
#
# ellucian_tomcat_db_hostname:
# ellucian_tomcat_db_port:
# ellucian_tomcat_db_sid:

# ellucian_tomcat_banproxy_password:
# ellucian_tomcat_banssuser_password:
#
# ellucian_tomcat_extra_libs_path:
#
# ellucian_wgetrc_http_password:
#
# ellucian_nfs_server:
# ellucian_nfs_remote_mount:
#
# ellucian_jenkins_authorize_key:
#
# ellucian_cacerts:
#
```

## Dependencies

Direct
 - [ChristopherDavenport.ellucian-tomcat](https://galaxy.ansible.com/ChristopherDavenport/ellucian-tomcat/)
 - [ChristopherDavenport.ellucian-wgetrc](https://galaxy.ansible.com/ChristopherDavenport/ellucian-wgetrc/)
 - [ChristopherDavenport.cacerts-import](https://galaxy.ansible.com/ChristopherDavenport/cacerts-import/)
 - [ChristopherDavenport.jenkins-slave](https://galaxy.ansible.com/ChristopherDavenport/jenkins-slave/)
 - [geerlingguy.nfs](https://galaxy.ansible.com/geerlingguy/nfs/)
 - [cmprescott.autofs](https://galaxy.ansible.com/cmprescott/autofs/)

Transitive
 - [ChristopherDavenport.universal-java](https://galaxy.ansible.com/ChristopherDavenport/universal-java/)
 - [ChristopherDavenport.universal-tomcat](https://galaxy.ansible.com/ChristopherDavenport/universal-tomcat/)


## Example Playbook

```yml
- hosts: yourhostname
  become: yes
  vars:
    ellucian_environment_name: TEST
    ellucian_wgetrc_http_password: fakeWgetRcPassword
    ellucian_tomcat_db_hostname: banner.test.school.edu
    ellucian_tomcat_db_port: "2322"
    ellucian_tomcat_db_sid: TEST
    ellucian_tomcat_banproxy_password: "fakeBanProxyPass"
    ellucian_tomcat_banssuser_password: "fakeBanSSUserPass"
    ellucian_tomcat_extra_libs_path:
      - "/home/fakeuser/lib/ojdbc6.jar"
      - "/home/fakeuser/lib/xdb6.jar"
    ellucian_nfs_server: jobsub.test.school.edu
    ellucian_nfs_remote_mount: /u02/ellucian/staging
    ellucian_jenkins_authorize_key: /home/fakeuser/jenkinsmaster.pub
    ellucian_cacerts:
      - name: EthosIdentity.pem
        alias: EthosIdentity
        location: remote
        server: ethosidentity.test.school.edu
        port: "9443"
  roles:
    - ChristopherDavenport.ellucian-appserver-tomcat
```
