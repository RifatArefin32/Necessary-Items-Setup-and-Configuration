### Start Apache2 Server
```
  sudo systemctl start apache2
```
### Stop Apache2 Server
```
  sudo systemctl stop apache2
```
### Restart Apache2 Server
```
  sudo systemctl restart apache2
```
### Reload Apache2 Configuration
```
  sudo systemctl reload apache2
```
### Check Apache2 Server Status
```
  sudo systemctl status apache2
```
### Enable Apache2 to Start on Boot
```
  sudo systemctl enable apache2
```
### Disable Apache2 from Starting on Boot
```
  sudo systemctl disable apache2
```
### Check Apache2 Configuration Syntax
```
  sudo apache2ctl configtest
```
### List Enabled Apache2 Modules
```
  sudo apache2ctl -M
```
### Enable an Apache2 Module
```
  sudo a2enmod <module_name>
```
  Example:
```
  sudo a2enmod rewrite
```
### Disable an Apache2 Module
```
  sudo a2dismod <module_name>
```
Example:
```
  sudo a2dismod rewrite
```
### Enable an Apache2 Site
```
  sudo a2ensite <site_name>
```
Example:
```
  sudo a2ensite example.com.conf
```
### Disable an Apache2 Site
```
  sudo a2dissite <site_name>
```
Example:
```
  sudo a2dissite example.com.conf
```
### View Apache2 Error Logs
```
  sudo tail -f /var/log/apache2/error.log
```
### View Apache2 Access Logs
```
  sudo tail -f /var/log/apache2/access.log
```
### Test Apache2 Configuration
```
  sudo apache2ctl -t
```
### Reload Apache2 Service (if systemctl is not available)
```
  sudo service apache2 reload
```
### Restart Apache2 Service (if systemctl is not available)
```
  sudo service apache2 restart
```
### List Available Sites
```
  ls /etc/apache2/sites-available/
```
### List Enabled Sites
```
  ls /etc/apache2/sites-enabled/
```
### Create a New Virtual Host File
```
  sudo nano /etc/apache2/sites-available/example.com.conf
```
Then add the virtual host configuration, save, and enable the site:
```
  sudo a2ensite example.com.conf
  sudo systemctl reload apache2
```
### Disable a Virtual Host
```
  sudo a2dissite example.com.conf
  sudo systemctl reload apache2
```
### Set Permissions for the Web Directory
```
  sudo chown -R www-data:www-data /var/www/html
  sudo chmod -R 755 /var/www/html
```
### Enable HTTPS with SSL Module
```
  sudo a2enmod ssl
  sudo systemctl restart apache2
```
### Generate a Self-Signed SSL Certificate
```
  sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
```
### Configure a Virtual Host for SSL
```
  sudo nano /etc/apache2/sites-available/default-ssl.conf
```
Add or modify the configuration for SSL, then enable the site and reload Apache2:
```
  sudo a2ensite default-ssl
  sudo systemctl reload apache2
```
