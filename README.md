# Ellucian Appserver Tomcat

[![Build Status](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-appserver-tomcat.svg?branch=master)](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-appserver-tomcat)

This is a single role to provision correctly tomcat appservers correctly for
Ellucian Banner 9 Applications.

A simple example playbook.

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
