Ansible-Role-Apache-Proxy
=========
This is a simple role which installs Apache as Proxy Server

Requirements
------------
None

Role Variables
--------------
\- apache_server_name: "server.example.com"  
\- apache_default_admin_email: "admin@example.com"  
\- apache_copy_ssl_files: true  
\- apache_ssl_certificate_file: 'files/vm.crt'  
\- apache_ssl_certificate_key_file: 'files/vm.key'   
\# If apache_copy_ssl_files is false you need to provide the following variables:  
\# - apache_ssl_cert_file_location  
\# - apache_ssl_cert_key_location  
\- apache_ssl_cert_file_location: "/etc/pki/tls/certs/vm.crt"  
\- apache_ssl_cert_key_location: "/etc/pki/tls/private/vm.key"  
\- apache_proxy_host: "localhost"  
\- apache_proxy_port: 8080  
\- default_context_path: "/"  

Dependencies
------------
None

Example Playbook
----------------
&nbsp;&nbsp;vars:  
&nbsp;&nbsp;&nbsp;&nbsp;apache_server_name: "server.exmaple.com"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_default_admin_email: "admin@exmaple.com"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_copy_ssl_files: false  
&nbsp;&nbsp;&nbsp;&nbsp;apache_ssl_cert_file_location: "/etc/letsencrypt/live/{{ apache_server_name }}/fullchain.pem"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_ssl_cert_key_location: "/etc/letsencrypt/live/{{ apache_server_name }}/privkey.pem"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_proxy_host: "localhost"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_proxy_port: 8080  
&nbsp;&nbsp;&nbsp;&nbsp;default_context_path: "/"

&nbsp;&nbsp;roles:
&nbsp;&nbsp;&nbsp;&nbsp;- ansible-role-apache-proxy

License
-------
MIT

Author Information
------------------
Islam Kambarov

