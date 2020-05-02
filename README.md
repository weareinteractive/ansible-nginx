# Ansible weareinteractive.nginx role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-nginx.svg)](https://travis-ci.org/weareinteractive/ansible-nginx)
[![Galaxy](http://img.shields.io/badge/galaxy-weareinteractive.nginx-blue.svg)](https://galaxy.ansible.com/weareinteractive/nginx)
[![GitHub Tags](https://img.shields.io/github/tag/weareinteractive/ansible-nginx.svg)](https://github.com/weareinteractive/ansible-nginx)
[![GitHub Stars](https://img.shields.io/github/stars/weareinteractive/ansible-nginx.svg)](https://github.com/weareinteractive/ansible-nginx)

> `weareinteractive.nginx` is an [Ansible](http://www.ansible.com) role which:
>
> * installs nginx
> * configures nginx
> * creates sites
> * enables/disables sites
> * optionally removes default host
> * adds rules
> * configures service

**Note:**

> Since Ansible Galaxy supports [organization](https://www.ansible.com/blog/ansible-galaxy-2-release) now, this role has moved from `franklinkim.nginx` to `weareinteractive.nginx`!

## Installation

Using `ansible-galaxy`:

```shell
$ ansible-galaxy install weareinteractive.nginx
```

Using `requirements.yml`:

```yaml
- src: weareinteractive.nginx
```

Using `git`:

```shell
$ git clone https://github.com/weareinteractive/ansible-nginx.git weareinteractive.nginx
```

## Dependencies

* Ansible >= 2.4
## Related (see example)

* [weareinteractive.openssl](https://github.com/weareinteractive/ansible-openssl)
* [weareinteractive.htpasswd](https://github.com/weareinteractive/ansible-htpasswd)

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---

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
#       cert_path: /etc/letsencrypt/live/sub.example.com
#       port: 443
#       key_name: mykey.key
#       cert_name: mycert.crt
#     rules: []
#     auth:
#       name: foo
#       file: foo
#     append: ''
#

# dependencies packages to install package
nginx_dependencies:
  - ca-certificates
  - gnupg2
# apt repository
nginx_repo: "deb http://nginx.org/packages/{{ ansible_distribution|lower }}/ {{ ansible_distribution_release }} nginx"
# apt repository key
nginx_repo_key: ABF5BD827BD9BF62
# package name (version)
nginx_package: nginx
# run as a less privileged user for security reasons.
nginx_user: www-data
# number or auto
nginx_worker_processes: 1
nginx_worker_connections: 1024
# default settings
nginx_sendfile: 'on'
nginx_tcp_nopush: 'on'
nginx_tcp_nodelay: 'on'
nginx_keepalive_timeout: 15
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

```yaml
---

- name: restart nginx
  service: name=nginx state=restarted
  when: nginx_service_state != 'stopped'

- name: reload nginx
  service: name=nginx state=reloaded
  when: nginx_service_state != 'stopped'

```

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

## Usage

This is an example playbook:

```yaml
---

- hosts: all
  become: yes
  roles:
    - weareinteractive.apt
    - weareinteractive.openssl
    - weareinteractive.htpasswd
    - weareinteractive.nginx
  vars:
    htpasswd:
      - name: foobar
        users:
          - { name: foobar, password: foobar }
    openssl_generate_csr: yes
    openssl_self_signed:
      - name: fooboar.local
        subject:
           C: DE
           ST: Bavaria
           L: Munich
           O: Foo Bar Inc
           CN: foobar.local
           emailAddress: null@foobar.local
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
    nginx_worker_processes: 1
    nginx_remove_default: yes
    # do not start service as we're running in docker
    nginx_service_state: stopped
    nginx_service_enabled: no

```


## Testing

```shell
$ git clone https://github.com/weareinteractive/ansible-nginx.git
$ cd ansible-nginx
$ make test
```

## Contributing
In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

*Note: To update the `README.md` file please install and run `ansible-role`:*

```shell
$ gem install ansible-role
$ ansible-role docgen
```

## License
Copyright (c) We Are Interactive under the MIT license.
