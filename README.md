# Common use-case nginx configurations

[Nginx](http://wiki.nginx.org/) is an event-driven webserver / reverse-proxy capable of handling many concurrent requests with relative ease. 

This repo provides some boilerplate examples and recipe for getting started at configuring nginx for common use-cases, e.g. serving static files fast and efficient. 

All recipe take best practice into account and try not to repeat mistakes outlined in [IfIsEvil](http://wiki.nginx.org/IfIsEvil) and [CommonPitfalls](http://wiki.nginx.org/Pitfalls). 

It is recommended to always use the latest stable version of nginx. At the time of this writing this is version 1.0.0. 

## Author

[Matthias Adler](http://matthiasadler.info/) (macedigital)

# Usage

* Put 'recipe', 'sites-available' and 'sites-enabled' folders into nginx configuration directory
* Pick an example vhost config and replace `server_name` and `root` directives with appropiate values 
* Symlink wanted vhost config in sites-enabled folder, make sure it ends with .conf 
* If not already done so, update your main nginx configuration file 'nginx.conf' with `include sites-enabled/*.conf`
* Reload nginx `killproc /usr/sbin/nginx -HUP`

# Credits 

Inspiration came from others having had similar ideas, most notably: 

* [perusio](https://github.com/perusio)
* [omega8cc](https://github.com/omega8cc/nginx-for-drupal)
* [yhager](https://github.com/yhager/nginx_drupal)

# Disclaimer

These recipe work for me and may not work for you. If you think you spotted an error or have suggestions for improvements just drop me a note. 

