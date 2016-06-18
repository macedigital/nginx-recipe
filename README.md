# Common use-case nginx configurations

[Nginx](http://wiki.nginx.org/) is an event-driven webserver / reverse-proxy capable of handling many concurrent requests with relative ease. 

This repo provides some boilerplate examples and recipe for getting started at configuring nginx for common use-cases, e.g. serving static files fast and efficient. 

All recipe take best practice into account and try not to repeat mistakes outlined in [IfIsEvil](http://wiki.nginx.org/IfIsEvil) and [CommonPitfalls](http://wiki.nginx.org/Pitfalls). 

It is recommended to always use the latest stable version of nginx. At the time of writing this is version **1.10.0**.

# Install

Clone this repo into the nginx configuration folder, or download a release and extract it's contents to `/etc/nginx`.

By default, it is assumed log-files are written to `/var/log/nginx`, cache files will be written to `/var/lib/nginx/` and the pid-file for the master process can be written to `/run/`.

# Usage


The `nginx.conf` file provides a fallback server on port 80 which catches all requests that could not be matched to a configured server-name, e.g. someone typed in the IP address of the host machine nginx is running on, while almost all known mime-types are included in `mime.types`.

The following configuration directory structure offers maximum re-usability and flexibility:

````
/etc/nginx/
├── conf.d
├── recipe
├── sites-available
└── sites-enabled
````

- conf.d
    - Files ending with `*.conf` will be loaded automatically and be global defaults.

- recipe
    - Contains boilerplate for common use-cases that are neither server, nor location dependent.

- sites-available
    - Full server configurations, utilizing one or more recipe and filling in the gaps with explicit location rules.

- sites-enabled
    - Any file ending with `*.conf` will be included in the nginx runtime configuration. Should only contain symlinks to configurations from `sites-available`.



In order to enable and use server-configuration, type the following:

`cd /etc/nginx/sites-enabled && ln -s ../static.example.com.conf && sudo nginx -s SIGHUP`

This command will create a new symlink with the same name as the file in `sites-available` and reload nginx to apply the server configuration immediately.

# Testing

Its always a good idea to test your configuration before reloading/restarting nginx. You'd be suprised how many people did a `service reload nginx` and not realizing that changes weren't in affect because the configuration files do not pass validation. 

`nginx -t` will instruct nginx to check for syntax and/or logical errors in your configuration. 

Some configuration options (http2 support, etc.) are only available in later versions of nginx, and/or require external libraries to be installed.

You can verify which nginx version you're currently using by typing `nginx -v` in a terminal. In case you're missing a module, `nginx -V` will show all configuration flags and compiled-in modules.

# Disclaimer

These recipe work for me and may not work for you. If you think you spotted an error or have suggestions for improvements just drop me a note.

Contributions are welcome!

# Credits

Inspiration came from others having had similar ideas, most notably:

* [perusio](https://github.com/perusio)
* [omega8cc](https://github.com/omega8cc/nginx-for-drupal)
* [yhager](https://github.com/yhager/nginx_drupal)
