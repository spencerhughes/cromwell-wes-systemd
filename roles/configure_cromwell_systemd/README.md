Configure Cromwell SystemD Service
=========

Installs the Cromwell application and sets up a SystemD service to manage it.

Requirements
------------

Role Variables
--------------

| Variable | Default | Description |
|----------|---------|-------------|
| cromwell_log_directory | /var/log/cromwell | Directory into which Cromwell logs will be placed. |
| cromwell_install_directory | /opt/cromwell | Directory into which the Cromwell JAR files will be installed. |
| cromwell_config_directory | /etc/cromwell | Directory into which the Cromwell application config will be installed. |
| cromwell_config_name | cromwell-application.conf | Name of the Cromwell config file |
| cromwell_job_outputs | /opt/cromwell/output | Directory into which Cromwell execution results will be placed. |
| cromwell_version | 85 | Version of Cromwell to install. |
| mysql_user | cromwell | Name of the MySQL user to use to connect to the database. |
| mysql_password | cromwell | Password for the MySQL user to use to connect to the database. |
| mysql_database_name | cromwell_db | Name of the MySQL database to connect to. |

Dependencies
------------

- create_cromwell_user

Example Playbook
----------------

    - hosts: all
      roles:
         - name: configure_cromwell_systemd
           vars:
             cromwell_log_directory: /var/log/cromwell
             cromwell_install_directory: /opt/cromwell
             cromwell_config_directory: /etc/cromwell
             cromwell_config_name: cromwell-application.conf
             cromwell_job_outputs: /opt/cromwell/output
             cromwell_version: 85
             mysql_user: cromwell
             mysql_user_password: cromwell
             mysql_database_name: cromwell_db

License
-------

GPLv2

Author Information
------------------

Spencer Hughes (spencer@somanydoors.ca)
