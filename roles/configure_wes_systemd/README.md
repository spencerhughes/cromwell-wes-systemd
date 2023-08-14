Configure WES SystemD Service
=========

Installs the Cromwell Workflow Execution Service application and sets up a SystemD service to manage it.

Requirements
------------

Role Variables
--------------

| Variable | Default | Description |
|----------|---------|-------------|
| wes_install_directory | /opt/cromwell | Directory into which the Cromwell Workflow Execution Service JAR file will be installed. |
| wes_log_directory | /var/log/cromwell | Directory into which Cromwell Workflow Execution Service logs will be placed. |
| wes_server_address | 127.0.0.1 | IP address to bind the WES service to. |
| wes_version | 1.0.0 | Version of the WES application to deploy. |

Dependencies
------------

- create_cromwell_user

Example Playbook
----------------

    - hosts: all
      roles:
         - name: configure_wes_systemd
           vars:
             wes_install_directory: /opt/cromwell
             wes_log_directory: /var/log/cromwell
             wes_server_address: 127.0.0.1
             wes_version: 1.0.0

License
-------

Author Information
------------------

