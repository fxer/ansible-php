## Ansible Role: php
Configure php and php-fpm on RedHat/CentOS 7 servers

## Tasks
* Install required php and php-fpm packages
* Configure php.ini
* Configure multiple php-fpm pools

## php-fpm
Setup by default to listen on a unix socket instead of a tcp port. Also handles setting up multiple pools, so you can have one per app instead of sharing.


Default settings (see `defaults/main.yml`):

    php_fpm_config_path: "/etc/php-fpm.d"
    php_fpm_run_path: "/var/run/php-fpm"
    php_fpm_listen_owner: "nginx"
    php_fpm_listen_group: "nginx"
    php_fpm_listen_mode: "0660"
    php_fpm_user: "nginx"
    php_fpm_group: "nginx"
    php_fpm_pm: "ondemand"
    php_fpm_pm_max_children: 10
    php_fpm_pm_process_idle_timeout: "10s"
    php_fpm_pm_max_requests: 100
    php_fpm_catch_workers_output: "yes"

If you would like to disable the default `www.conf` that is installed on CentOS set this to `True`:

    php_fpm_disable_default_pool: False

Define your php-fpm pools. Additionally you can override any `php_fpm_*` variable on a per-pool basis. The top level key will create a pool named as `<key>.conf`. It will use all the role default values unless you choose to override them.

    php_fpm_pools:
      www:
        php_fpm_pm_max_children: 20
        php_fpm_pm: dynamic
      myapp:
      myapp2:
        php_fpm_user: "apache"
        php_fpm_group: "apache"

## License
2-clause BSD
