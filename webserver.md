# Example webserver with vhosts and Let's Encrypt certs

## Requirements

* [nginx](https://github.com/morbidick/ansible-role-nginx)
* [nginx-vhosts](https://github.com/morbidick/ansible-role-nginx-vhosts)
* [certbot](https://github.com/morbidick/ansible-role-certbot)

## Playbook

The `certbot` role needs to be run in between `nginx` and `nginx-vhosts` so that Nginx is setup and serving the challenge directory and the created vhosts have their certs available.

````yaml
- hosts: all
  become: yes

  roles:
  - nginx
  - certbot
  - nginx-vhosts

  vars:
    nginx_default_page_content: "<h1>Welcome to this newly configured webserver!</h1>"
    certbot_mail: me@example.com
    vhosts:
      - host: example.com
        type: static
    nginx_vhosts: "{{ vhosts }}"
    certbot_certs: "{{ vhosts }}"
````
