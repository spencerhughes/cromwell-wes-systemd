# Ansible Playbook to Deploy Cromwell

This Ansible playbook will deploy Cromwell and the DNAstack Workflow Execution Service to a host running a Debian-based distribution. It has been tested on Debian 12.

This playbook initializes the resources described in [DNAstack's on-premises engine documentation](https://docs.dnastack.com/docs/on-premises) as systemd services. It will create services for:

- [Cromwell](https://github.com/broadinstitute/cromwell) running in server mode
- [MariaDB](https://mariadb.org/) database for storing Cromwell run information
- [DNAstack's WES service](https://github.com/DNAstack/cromwell-wes-service), which will allow interacting with Cromwell via GA4GH APIs
- [nginx](https://www.nginx.com/), which will act as a reverse proxy for the WES service

This playbook will start the services and configure them to start automatically at boot.

## Requirements

- `python3.5+`

## Setup

1. Create and activate a new Python virtual environment
    ```bash
    python3 -m venv ansible
    source ansible/bin/activate
    ```
0. Install Ansible using pip
    ```bash
    python3 -m pip install ansible
    ```
0. Set the following required variables in [host_vars/localhost.yml](host_vars/localhost.yml):
    - `client_key_local_path`: The path to the directory on the local machine that will contain the client key file.
    - `client_cert_local_path`: The path to the directory on the local machine that will contain the client certificate file.

    Other variables in this file may be configured as desired.

0. Install required collections
    ```bash
    ansible-galaxy install -r requirements.yml
    ```

## Usage

### Installation

Run `ansible-playbook playbook.yml` to setup MySQL, Cromwell, nginx, and DNAstack WES's service locally.

### Uninstallation

***This playbook is a work in progress and has not been tested. Use at your own risk.***

1. Edit [uninstall.yml](uninstall.yml) and set the following variables based on what components you'd like to uninstall:

    - `uninstall_java`
    - `remove_logs`
    - `uninstall_nginx`
    - `restore_nginx_conf`
    - `remove_keys`
    - `uninstall_mysql`
    - `remove_db`
    - `remove_db_user`
    - `uninstall_python_mysql`
    - `uninstall_build_essential`
    - `uninstall_python3_dev`
    - `uninstall_pkgconfig`
    - `uninstall_cromwell`
    - `remove_job_output_dir`
    - `uninstall_wes`

    ***Note:*** Setting `restore_nginx_conf` to true will restore the earliest backup of `/etc/nginx/nginx.conf`. If any changes have been made to `nginx.conf` outside of Ansible, these changes will be overwritten. A backup of the pre-reversion `nginx.conf` will be taken as part of the uninstall process.

0. Run `ansible-playbook uninstall.yml`.

### Managing Installed Services

The services installed by this playbook are named:

- `cromwell`
- `wes`
- `mysql`
- `nginx`

These services can be managed using `systemctl` and `journalctl`. Examples of some common administrative tasks are provided below:

```bash
# Get service status
systemctl status ${service}

# Stop a service
systemctl stop ${service}

# Start a service
systemctl start ${service}

# Restart a service
systemctl restart ${service}

# Get logs for a service
sudo journalctl -u ${service}
```

### Connecting the engine to Workbench

Once the services have been deployed, the variables required for connecting the Cromwell engine on Workbench will be printed to the console. They may also be printed to stdout at any time by running the following command:

```bash
ansible-playbook -t workbench_config playbook.yml
```
