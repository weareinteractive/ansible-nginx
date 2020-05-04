<a name="2.0.1"></a>
### 2.0.1 (2020-05-04)




<a name="2.0.0"></a>
## 2.0.0 (2020-05-04)


#### Features

*   move files to fit conventions ([fc20b264](https://github.com/weareinteractive/ansible-nginx/commit/fc20b2640014d08192c8b0000e5898de4969bf7b))

#### Breaking changes

In order to upgrade from 1.x to 2.x you need to:

* add extensions to `nginx_sites[].ssl.key_name` and `nginx_sites[].ssl.cert_name` i.e. `server.key`
* in case of custom rules, change the location from `files/etc-nginx-rules` to `files/etc/nginx/rules`

<a name="1.5.0"></a>
## 1.5.0 (2019-10-18)


#### Features

*   rename role ([95bb2d51](https://github.com/weareinteractive/ansible-nginx/commit/95bb2d51398f6e61c6330d2378a38e29438569c3))
*   ensure config folders ([e27ebc86](https://github.com/weareinteractive/ansible-nginx/commit/e27ebc86c522fff78c088b84ca6e411ec93854e4))
*   add depencies ([299f3844](https://github.com/weareinteractive/ansible-nginx/commit/299f38446f76359ca85d75db91cb7adcaca22f2e))
*   ensure sites-enabled folder ([731d3546](https://github.com/weareinteractive/ansible-nginx/commit/731d354692b6c98af0412a8e97b89888cbb46dc2))
*   bump ansible min version ([67b2c245](https://github.com/weareinteractive/ansible-nginx/commit/67b2c245f3f4594595fb281b9352295daa861e9a))
*   update apt repository ([95a17572](https://github.com/weareinteractive/ansible-nginx/commit/95a17572b23145f68ee9376d4604093d967ad7af))
*   use import_tasks ([0f2ad490](https://github.com/weareinteractive/ansible-nginx/commit/0f2ad4906914081ac244c707f7b3b221382edd79))

#### Bug Fixes

*   add apt key ([fe5c5ca6](https://github.com/weareinteractive/ansible-nginx/commit/fe5c5ca66aaa7d6dc6e64be7f67b22636fd99637))



<a name="1.4.0"></a>
## 1.4.0 (2016-08-15)


#### Features

*   readd restart handler ([6cb85d7d](https://github.com/weareinteractive/ansible-nginx/commit/6cb85d7d08d206a5d35fef833ac6974228a62dc7))
*   use reload instead of restart ([8dd51d3f](https://github.com/weareinteractive/ansible-nginx/commit/8dd51d3fe4dfbf5a6b843562d5f4995810dd121f))



<a name="1.3.0"></a>
## 1.3.0 (2016-07-27)


#### Features

*   update syntax for ansible 2.0 ([669ceaf9](https://github.com/weareinteractive/ansible-nginx/commit/669ceaf9cdf3bef2d4b4d71bab0db75d6fa89019))
*   add CHANGELOG ([34ed15ac](https://github.com/weareinteractive/ansible-nginx/commit/34ed15ac8998e491c8f79a1311ddca518f5c0899))



