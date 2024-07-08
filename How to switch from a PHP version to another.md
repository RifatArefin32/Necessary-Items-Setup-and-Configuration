Suppose we want to switch from PHP 8.0 to PHP 8.3. To switch to PHP 8.3 on our Ubuntu system and configure Apache to use it, follow these steps:

## Add the PHP 8.3 Repository
```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt update
Install PHP 8.3:
```
```bash
sudo apt install php8.3
Install PHP 8.3 Modules (Optional):
```

## Install any additional PHP modules we might need
```bash
sudo apt install php8.3-cli php8.3-common php8.3-fpm php8.3-mysql php8.3-xml php8.3-mbstring php8.3-curl
Disable PHP 8.0 and Enable PHP 8.3 for Apache:
```
```bash
sudo a2dismod php8.0
sudo a2enmod php8.3
```

## Update the update-alternatives Configuration if necessary
This allows you to switch between PHP versions more easily.
```bash
sudo update-alternatives --set php /usr/bin/php8.3
sudo update-alternatives --set phar /usr/bin/phar8.3
sudo update-alternatives --set phar.phar /usr/bin/phar.phar8.3
sudo update-alternatives --set phpize /usr/bin/phpize8.3
sudo update-alternatives --set php-config /usr/bin/php-config8.3
```
## Restart Apache
```bash
sudo systemctl restart apache2
```

## Verify PHP Version
Ensure that Apache is now using PHP 8.3.
```bash
php -v
```

## Check Apache Configuration:
Create a PHP file to verify the PHP version running on your server.
```bash
sudo nano /var/www/html/info.php
```

## Add the following content to info.php:
```php
<?php phpinfo(); ?>
```
Save the file and exit. Then, open your web browser and navigate to http://your-server-ip/info.php. We should see a page displaying the PHP version and other details. Confirm that it shows PHP 8.3.
<br>
After completing these steps, our Ubuntu system should be running PHP 8.3, and Apache should be configured to use PHP 8.3.
