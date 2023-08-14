Configure MySQL
=========

Installs MariaDB and configures it for Cromwell.

Requirements
------------

None.

Role Variables
--------------

| Variable | Default | Description |
|----------|---------|-------------|
| mysql_user | cromwell | User to be created for Cromwell use. |
| mysql_user_password | cromwell | Password for Cromwell user. ***This should be encrypted using `ansible-vault` in production.*** |
| mysql_root_password | cromwell | Password for MySQL root user. ***This should be encrypted using `ansible-vault` in production.*** |
| mysql_database_name | cromwell_db | Name of the database to be created for Cromwell. |

Dependencies
------------

Example Playbook
----------------

License
-------

Author Information
------------------

