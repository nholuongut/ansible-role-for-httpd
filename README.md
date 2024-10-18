# Install and configure httpd on your system

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/nholuongut/ansible-role-for-httpd/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars_files:
    - ../../vars/main.yml
    - ../../defaults/main.yml

  roles:
    - role: robertdebock.httpd
      # https_ssl_enable: yes
      httpd_port: 8080
      httpd_ssl_port: 8443
      httpd_locations:
        - name: my_location
          location: /my_location
          backend_url: "http://localhost:8080/myapplication"
      # httpd_vhosts:
      #   - name: my_vhost_docroot
      #     servername: www1.example.com
      #     documentroot: "{{ httpd_data_directory }}/www1.example.com"
      #   - name: my_vhost_backend_http
      #     servername: www2.example.com
      #     backend_url: "http://www.example.com/"
      #     serveralias:
      #       - example.com
      #       - www.example.com
      #   - name: my_vhost_remote
      #     servername: www3.example.com
      #     remote: "http://localhost:3128/"
      #   - name: my_vhost_backend_https
      #     servername: www4.example.com
      #     backend_url: "https://www.example.com/"
      #   - name: my_vhost_piratebay
      #     servername: piratebay.nl
      #     backend_url: "https://thepirate-bay.org/"
      #     proxy_preserve_host: Off
      #     proxy_requests: Off
      #     setenv:
      #       - name: force-proxy-request-1.0
      #         value: 1
      #       - name: proxy-nokeepalive
      #         value: 1
      #       - name: proxy-initial-not-pooled
      #       - name: proxy-sendchunks
      #         value: 1
      #   - name: no_doc_root
      #     servername: nodocroot.example.com
      #     documentroot: /var/www/html/nodocroot
      #     create_docroot: no
      httpd_directories:
        - name: my_directory
          path: "{{ httpd_data_directory }}/my_directory"
          # options:
          #   - Indexes
          #   - FollowSymLinks
          allow_override: All
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/nholuongut/ansible-role-for-httpd/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.buildtools
    - role: robertdebock.python_pip
    - role: robertdebock.openssl
      openssl_items:
        - name: apache-httpd
          common_name: "{{ ansible_fqdn }}"
```

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/nholuongut/ansible-role-for-httpd/blob/master/defaults/main.yml):

```yaml
---
# defaults file for httpd

# The servername to use.
httpd_servername: "{{ ansible_fqdn }}"

# The non-SSL port to use.
httpd_port: 80

# Enable (self-signed certificates) SSL?
https_ssl_enable: no

# To configure https, set the hostname to listen to.
httpd_ssl_servername: "{{ ansible_fqdn }}"

# For SSL a TCP port is required.
httpd_ssl_port: 443

# SSL Certificate:
httpd_openssl_crt: "{{ httpd_openssl_crt_directory }}/apache-httpd.crt"

# SSL Key
httpd_openssl_key: "{{ httpd_openssl_key_directory }}/apache-httpd.key"

# If the "it works" page should be kept
httpd_remove_example: no
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/nholuongut/ansible-role-for-httpd/blob/master/requirements.txt).


The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟