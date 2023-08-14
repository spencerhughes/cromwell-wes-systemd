# Ansible Playbook to Deploy Cromwell

This Ansible playbook will deploy Cromwell and the DNAstack Workflow Execution Service to a host running a Debian-based distribution. It has been tested on Debian 12.

This playbook initializes the resources described in [DNAstack's on-premises engine documentation](https://docs.dnastack.com/docs/on-premises) as systemd services. It will create services for:

- [Cromwell](https://github.com/broadinstitute/cromwell) running in server mode
- [MariaDB](https://mariadb.org/) database for storing Cromwell run information
- [DNAstack's WES service](https://github.com/DNAstack/cromwell-wes-service), which will allow interacting with Cromwell via GA4GH APIs
- [nginx](https://www.nginx.com/), which will activate as a reverse proxy for the WES service

This playbook will start the services and configure them to start automatically at boot.

## Requirements

- `python3.5+`
