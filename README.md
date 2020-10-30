Ansible-Certbot-Apache-Proxy
=========
Install Certbot and Apache as Proxy Server

Example Playbook
----------------
\---  
\- hosts: all  
&nbsp;&nbsp;become: yes  

&nbsp;&nbsp;vars:  
&nbsp;&nbsp;&nbsp;&nbsp;apache_create_vhosts: false  
&nbsp;&nbsp;&nbsp;&nbsp;apache_remove_default_vhost: true  
&nbsp;&nbsp;&nbsp;&nbsp;certbot_admin_email: "admin@example.com"  
&nbsp;&nbsp;&nbsp;&nbsp;certbot_create_if_missing: true  
&nbsp;&nbsp;&nbsp;&nbsp;certbot_create_standalone_stop_services:  
&nbsp;&nbsp;&nbsp;&nbsp;\- httpd  
&nbsp;&nbsp;&nbsp;&nbsp;certbot_certs:  
&nbsp;&nbsp;&nbsp;&nbsp;\- domains:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- "jenkins.example.com"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_server_name: "jenkins.example.com"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_default_admin_email: "admin@example.com"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_copy_ssl_files: false  
&nbsp;&nbsp;&nbsp;&nbsp;apache_ssl_cert_file_location: "/etc/letsencrypt/live/{{ apache_server_name }}/fullchain.pem"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_ssl_cert_key_location: "/etc/letsencrypt/live/{{ apache_server_name }}/privkey.pem"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_proxy_host: "localhost"  
&nbsp;&nbsp;&nbsp;&nbsp;apache_proxy_port: 8080  
&nbsp;&nbsp;&nbsp;&nbsp;default_context_path: "/"  

&nbsp;&nbsp;pre_tasks:  
&nbsp;&nbsp;&nbsp;&nbsp;\- name: Update apt cache  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;apt:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;update_cache: true  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cache_valid_time: 600  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;when: ansible_os_family == 'Debian'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;changed_when: false  

&nbsp;&nbsp;&nbsp;&nbsp;\- name: Install cron (Debian)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;apt:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name: cron  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;state: present  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;when: ansible_os_family == 'Debian'  

&nbsp;&nbsp;&nbsp;&nbsp;\- name: Install dependencies (RedHat)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yum:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- cronie  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\- epel-release  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;when: ansible_os_family == 'RedHat'  

&nbsp;&nbsp;roles:  
&nbsp;&nbsp;&nbsp;&nbsp;\- ansible-role-apache  
&nbsp;&nbsp;&nbsp;&nbsp;\- ansible-role-certbot  
&nbsp;&nbsp;&nbsp;&nbsp;\- ansible-role-apache-proxy  

