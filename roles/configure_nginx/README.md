Configure Nginx for WES
=========

Creates server and client certificates and configures Nginx to use them to serve the WES via proxy.

Requirements
------------

None.

Role Variables
--------------

| Variable | Default | Description |
|----------|---------|-------------|
| server_key_path | /etc/ssl/private | Path of private key for server SSL certificate. |
| server_key_name | cromwell-selfsigned.key | Name of private key for server SSL certificate. |
| server_key_password | Key is unencrypted | Passphrase to use to encrypt the server SSL private key. ***This should be encrypted using `ansible-vault` in production.*** |
| server_cert_path | /etc/ssl/certs | Path of server self-signed certificate. |
| server_cert_name | cromwell-selfsigned.crt | Name of the self-signed certificate. |
| server_cert_common_name | None (Public IP is autodetected and used if not set) | Common name for the self-signed certificate CSR |
| server_cert_alt_names | None (Public IP and localhost are added if not set) | List of alternate names to allow the certificate to be used for. |
| server_org_name | Self-signed certificate | Organization name to register on the certificate. |
| server_country_name | XX | Country code for self-signed certificate. |
| server_state_or_province_name | N/A | State or provice for self-signed certificate. |
| server_locality_name | N/A | Locality name for self-signed certificate. |
| client_key_local_path | None | Path on the control node of client private key. Playbook will fail unless set. |
| client_key_name | cromwell-client.key | Name of client private key. |
| client_key_passphrase | Key is unencrypted | Passphrase to use to encrypt the client private key. ***This should be encrypted using `ansible-vault` in production.*** |
| client_cert_common_name | Local Cromwell: Self-signed certificate | Common name for the client certificate CSR. |
| client_org_name | Value of `server_org_name` | Organization name for client certificate. |
| client_country_name | Value of `server_country_name` | Country name for client certificate. |
| client_state_or_province_name | Value of `server_state_or_province_name` | State or province name for client certificate. |
| client_locality_name | Value of `server_locality_name` | Locality name for client certificate. |
| client_cert_local_path | None | Path on the control node of the client certificate. Playbook will fail unless set. |
| client_cert_path | Value of `server_cert_path` | Path on the server of the client certificate. |
| client_cert_name | cromwell-client.crt | Name of the client self-signed certificate. |

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: all
      roles:
        - role: configure_nginx
          vars:
            server_key_path: /etc/ssl/private
            server_key_name: cromwell-selfsigned.key
            server_cert_path: /etc/ssl/certs
            server_cert_name: cromwell-selfsigned.crt
            server_org_name: Self-signed certificate
            server_country_name: XX
            server_state_or_province_name: N/A
            server_locality_name: N/A
            client_key_name: cromwell-client.key
            client_cert_common_name: "Local Cromwell: Self-signed certificate"
            client_org_name: Self-signed certificate
            client_country_name: XX
            client_state_or_province_name: N/A
            client_locality_name: N/A
            client_cert_name: cromwell-client.crt
            nginx_worker_processes: 1
            nginx_worker_connections: 1024
            client_key_local_path: /home/user
            client_cert_local_path: /home/user

License
-------

GPLv2

Author Information
------------------

