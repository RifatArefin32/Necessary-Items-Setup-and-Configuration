# Setting up and installing Moodle on a Linux server

## 1. Prepare Your Server
Ensure your server is up to date:
```bash
sudo apt update
sudo apt upgrade
```
## 2. Install Required Software
Moodle requires a web server, a database server, and PHP. You can use Apache, MySQL, and PHP for this setup.
### Install Apache
```bash
sudo apt install apache2
```
### Install MySQL
```bash
sudo apt install mysql-server
sudo mysql_secure_installation
```
**Note:**
The `sudo mysql_secure_installation` command is a script provided by MySQL to improve the security of your MySQL installation. It guides you through several steps to configure your MySQL database server securely. Here's what it typically does:
- Set a Password for the MySQL Root User: If you haven't already set a password for the MySQL root user, this script will prompt you to set one. The root user is the administrative account for MySQL.
- Remove Anonymous Users: By default, MySQL installations allow anonymous users. The script can remove these users to prevent unauthorized access.
- Disallow Root Login Remotely: To increase security, the script offers to disallow remote login for the root user, ensuring that root can only connect from localhost.
- Remove Test Database: MySQL installations include a test database by default, which is accessible by all users. The script can delete this database to prevent potential misuse.
- Reload Privilege Tables: The script will prompt you to reload the privilege tables to ensure that all changes take effect immediately.
Running mysql_secure_installation is recommended after installing MySQL to help lock down your database server against unauthorized access.


### Install PHP
Moodle requires specific PHP extensions. Install them along with PHP:
```bash
sudo apt install php libapache2-mod-php php-mysql php-xml php-zip php-intl php-mbstring php-gd php-curl php-xmlrpc php-soap
```

## 3. Create a Database for Moodle
### Log in to MySQL:
```bash
sudo mysql -u root -p
```
### Create a database and user for Moodle:
```sql
CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
```sql
CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY 'yourpassword';
```
```sql
GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
```
```sql
FLUSH PRIVILEGES;
EXIT;
```

## 4. Download Moodle
### Navigate to the web root directory and download the latest stable release of Moodle:
```bash
cd /var/www/html
sudo wget https://download.moodle.org/download.php/direct/stable39/moodle-latest-39.tgz
```
### Extract the downloaded file:
```bash
sudo tar -zxvf moodle-latest-39.tgz
```
## 5. Set Up Moodle Directory
Create a Moodle data directory:
```bash
sudo mkdir /var/moodledata
sudo chown -R www-data:www-data /var/moodledata
sudo chmod -R 775 /var/moodledata
```
### Set the correct permissions for the Moodle web directory:
```bash
sudo chown -R www-data:www-data /var/www/html/moodle
sudo chmod -R 755 /var/www/html/moodle
```
## 6. Configure Apache for Moodle
Create an Apache configuration file for Moodle:
```bash
sudo nano /etc/apache2/sites-available/moodle.conf
```
Add the following configuration:
```apache
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/moodle
    ServerName example.com

    <Directory /var/www/html/moodle>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/moodle_error.log
    CustomLog ${APACHE_LOG_DIR}/moodle_access.log combined

    <Directory /var/moodledata>
        Require all denied
    </Directory>
</VirtualHost>
```
### Enable the new site and the rewrite module:
```bash
sudo a2ensite moodle.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
```
## 7. Run Moodle Installation Script
Navigate to your Moodle site in a web browser and follow the on-screen instructions to complete the installation:
```arduino
http://example.com
```
Replace example.com with your domain or server IP address. Follow the steps to configure Moodle and provide the database details you created earlier.

## 8. Post-Installation Steps
Once the installation is complete, you might want to secure your site and perform additional configurations such as setting up SSL, configuring cron jobs, and optimizing performance.
### To set up SSL, you can use Let's Encrypt:
```bash
sudo apt install certbot python3-certbot-apache
sudo certbot --apache -d example.com
```
To configure cron jobs for Moodle:
```bash
sudo crontab -u www-data -e
```
Add the following line to run the cron script every minute:
```bash
* * * * * /usr/bin/php /var/www/html/moodle/admin/cli/cron.php > /dev/null
```
This should give you a working Moodle installation on your Linux server.
