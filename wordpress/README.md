## WordPress

This project comes with WordPress 4.2.2 pre-installed.

It also includes the following software:

- LAMP stack
  - Apache 2.4.7 with mod-php set up
  - MySQL 5.5
  - PHP 7.0.12 (Composer 1.0)

### Famous 5-minute install

You will have to go through the "Famous 5-Minute Install" by previewing your app (go to `Preview > Port 3000` from the IDE menu). This will allow you to enter your site title and create a WordPress administrator account.

Refer to this [guide](https://codex.wordpress.org/Installing_WordPress#Famous_5-Minute_Install) for more detailed instructions.

### Where is the WordPress directory?

WordPress has been installed into `/home/nitrous/code/public_html` folder.

### Customizing the server setup

Apache has been set up to listen to port 3000 and serves the contents of `/home/nitrous/code/public_html`.

You can customize mod-php settings by editing `/etc/php5/apache2/php.ini`. Server settings can be changed by editing `/etc/apache2/sites-available/000-default.conf`.

Remember to restart Apache with `sudo service apache2 restart` after editing those files so that your changes are applied.

