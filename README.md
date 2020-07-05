# Configure nginx vhosts with Ansible

[![Build Status](https://travis-ci.org/morbidick/ansible-role-nginx-vhosts.svg?branch=master)](https://travis-ci.org/morbidick/ansible-role-nginx-vhosts)

## Requirements

Nginx needs to be installed and configured, many vars and assumptions are tightly coupled with this [nginx role](https://github.com/morbidick/ansible-role-nginx). For Lets Encrypt support the [certbot role](https://github.com/morbidick/ansible-role-certbot) is required.

See [the full example](./webserver.md) for a complete playbook.

## Example playbook

````yaml
- hosts: all
  become: yes

  roles:
  - nginx
  - nginx-vhosts

  vars:
    nginx_vhosts:
    # static host serving the files under /var/www/example.com
    - host: example.com
      type: static
    # to proxy an upstream
    - host: proxy.example.com
      type: proxy
      # use type proxy-ws for websocket support
      target: http://localhost:3000
    # redirect to another domain
    - host: redirect.example.com
      type: redirect
      target: https://mysite.com
    # redirect to the www subdomain
    - host: example2.com
      type: redirect
      target: www
    # redirect to the domain without www
    - host: www.example.com
      type: redirect
      target: no-www
    # remove an upstream
    - host: www.example.com
      type: disabled
````

## Role variables

None of the variables below are required.

| Variable                 | Default   | Comment |
| :---                     | :---      | :---    |

For all options see [defaults/main.yml](defaults/main.yml)

## Development

You can use the [Vagrantfile](Vagrantfile) for local testing, just install vagrant and virtualbox and execute the following commands:

````bash
vagrant up
vagrant provision
````

## TODO
* locations support

## License

MIT
