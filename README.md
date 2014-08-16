# Ansible Nginx Role

[![Build Status](https://travis-ci.org/weareinteractive/ansible-role-nginx.png?branch=master)](https://travis-ci.org/weareinteractive/ansible-role-nginx)
[![Stories in Ready](https://badge.waffle.io/weareinteractive/ansible-role-nginx.svg?label=ready&title=Ready)](http://waffle.io/weareinteractive/ansible-role-nginx)

> `nginx` is an [ansible](http://www.ansible.com) role which: 
> 
> * installs nginx
> * configures nginx
> * enables/disables sites
> * optionally removes default host

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.nginx
```

Using `arm` ([Ansible Role Manager](https://github.com/mirskytech/ansible-role-manager/)):

```
$ arm install franklinkim.nginx
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-role-nginx.git
```

## Variables

```
# use repo to install latest git
nginx_latest: no
# lastest git repo path
nginx_latest_repo: ppa:nginx/stable
# run as a less privileged user for security reasons.
nginx_user: www-data
nginx_worker_processes: 'auto'
nginx_worker_connections: 768
# default settings
nginx_sendfile: 'on'
nginx_tcp_nopush: 'on'
nginx_tcp_nodelay: 'on'
nginx_keepalive_timeout: 54
nginx_types_hash_max_size: 2048
nginx_server_tokens: 'off'
# remove default site
nginx_remove_default: no
# start on boot
nginx_service_enabled: yes
# current state: started, stopped
nginx_service_state: started
```

## Example playbook

```
- host: all
  roles: 
    - franklinkim.nginx
  vars:
    nginx_latest: yes
    nginx_remove_default: yes
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-role-nginx.git
$ cd ansible-role-nginx
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
