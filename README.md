docker_ubuntu12.04_apache2_php5
===============================

This image uses

- ubuntu 12.04
- apache2
- php5 (with libapache2-mod-php5 and php5-mysql)

it enables the apache2-mods

- php5 (mod_php5)
- rewrite (mod_rewrite)

and exposes this port

- 80

user and group of the running apache2-process are both

- `www-data`.

the following apache config (VirtualHost) is used

    <VirtualHost *:80>
        ServerAdmin webmaster@localhost
    
        DocumentRoot /var/www/my_website/public_html
        <Directory /var/www/my_website/public_html/>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Order deny,allow
            Allow from all
        </Directory>
    
    </VirtualHost>

This enables you to run this container as follows:

    sudo docker run -d -p 80:80 -v <path_to_your_webapp>:/var/www/my_website/public_html --link <another_container>:<link_name> --name <container_name> <name_of_this_image>:<tag>

`<path_to_your_webapp>` is used as a volume. This is where your files should be (php-, html-, css-, js-files, etc). If your application needs write permission on some files or directories, you can change the owner (user and/or group) of those.

you could create a link to another container using `--link` (optional). e.g. a container hosting a DBMS (`--link database_container:db`)