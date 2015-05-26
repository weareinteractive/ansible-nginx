# Ansible Nginx Role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-nginx.svg)](https://travis-ci.org/weareinteractive/ansible-nginx)
[![Galaxy](http://img.shields.io/badge/galaxy-franklinkim.supervisor-blue.svg)](https://galaxy.ansible.com/list#/roles/1922)
[![GitHub Tags](https://img.shields.io/github/tag/weareinteractive/ansible-nginx.svg)](https://github.com/weareinteractive/ansible-nginx)
[![GitHub Stars](https://img.shields.io/github/stars/weareinteractive/ansible-nginx.svg)](https://github.com/weareinteractive/ansible-nginx)

> `nginx` is an [ansible](http://www.ansible.com) role which:
>
> * installs nginx
> * configures nginx
> * creates sites
> * enables/disables sites
> * optionally removes default host
> * adds rules
> * configures service

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.nginx
```

Using `requirements.yml`:

```
- src: franklinkim.nginx
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-nginx.git franklinkim.nginx
```

## Dependencies

* Ansible 1.9

## Related (see example)

* [franklinkim.openssl](https://github.com/weareinteractive/ansible-openssl)
* [franklinkim.htpasswd](https://github.com/weareinteractive/ansible-htpasswd)

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# nginx_sites:
#   - id: foo (required)
#     name: foo.com (required)
#     ip: '*'
#     port: 80
#     state: present
#     add_webroot: no
#     template: path/to/template.j2
#     aliases: []
#     redirects: []
#     ssl:
#       port: 443
#       key_name: mykey
#       cert_name: mycert
#     rules: []
#     auth:
#       name: foo
#       file: foo
#     append: ''
#

# apt repository
nginx_repo: ppa:nginx/stable
# package name (version)
nginx_package: nginx
# run as a less privileged user for security reasons.
nginx_user: www-data
# number or auto
nginx_worker_processes: 1
nginx_worker_connections: 768
# default settings
nginx_sendfile: 'on'
nginx_tcp_nopush: 'on'
nginx_tcp_nodelay: 'on'
nginx_keepalive_timeout: 65
nginx_types_hash_max_size: 2048
nginx_server_names_hash_bucket_size: 128
nginx_server_tokens: 'off'
# remove default site
nginx_remove_default: no
# start on boot
nginx_service_enabled: yes
# current state: started, stopped
nginx_service_state: started
# enabled/disabled sites
nginx_sites: []
# add rules
nginx_add_rules: yes
```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

* `restart nginx`

## Rules

If `nginx_add_rules` is `yes`, it will copy some configuration rules to `/etc/nginx/rules`:

* cache_busting.conf
* cors_web_fonts.conf
* gzip.conf
* no_transform.conf
* ssl.conf
* cors_ajax.con
* expires.conf
* gzip_static.conf
* security.conf

These can be included into your site definitions.

## Example playbook

```
- hosts: all
  sudo: yes
  roles:
    - franklinkim.openssl
    - franklinkim.htpasswd
    - franklinkim.nginx
  vars:
    nginx_worker_processes: 1
    nginx_remove_default: yes
    htpasswd:
      - name: foobar
        users:
          - { name: foobar, password: foobar }
    openssl_self_signed:
      - { name: 'foobar.local', country: 'DE', state: 'Bavaria', city: 'Munich', organization: 'Foo Bar', email: 'foo@bar.com' }
    nginx_sites:
      - id: foobar
        add_webroot: yes
        name: foobar.local
        ssl:
          key_name: foobar.local
          cert_name: foobar.local
        rules:
          - gzip
          - security
        auth:
          name: Foo Bar
          file: foobar
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-nginx.git
$ cd ansible-nginx
$ vagrant up
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License
Copyright (c) We Are Interactive under the MIT license.
