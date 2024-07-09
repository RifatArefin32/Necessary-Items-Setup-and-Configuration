Here are some essential commands for managing the Apache2 web server on an Ubuntu system:

# Installation and Basic Commands

### Install Apache2

```bash
sudo apt update
sudo apt install apache2
```

### Start Apache2

```bash
sudo systemctl start apache2
```

### Stop Apache2

```bash
sudo systemctl stop apache2
```

### Restart Apache2

```bash
sudo systemctl restart apache2
```

### Reload Apache2 (for changes in configuration files)

```bash
sudo systemctl reload apache2
```

### Enable Apache2 to Start on Boot

```bash
sudo systemctl enable apache2
```

### Disable Apache2 from Starting on Boot

```bash
sudo systemctl disable apache2
```

### Check Apache2 Status

```bash
sudo systemctl status apache2
```

# Managing Sites

## Enable a Site Configuration:

```bash
sudo a2ensite your_site.conf
```

## Disable a Site Configuration:

```bash
sudo a2dissite your_site.conf
```

## List Enabled Sites:

```bash
ls /etc/apache2/sites-enabled/
```

## List Available Sites:

```bash
ls /etc/apache2/sites-available/
```

# Managing Modules

### Enable an Apache Module:

```bash
sudo a2enmod module_name
```

### Disable an Apache Module:

```bash
sudo a2dismod module_name
```

### List Enabled Modules:

```bash
apache2ctl -M
```

# Configuration Files

### Apache2 Main Configuration File
```bash
sudo nano /etc/apache2/apache2.conf
```

### Default Site Configuration File
```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

# Additional Configuration Files:

### Ports Configuration
```bash
sudo nano /etc/apache2/ports.conf
```

### Environment Variables
```bash
sudo nano /etc/apache2/envvars
```

# Log Files

### Access Log
```bash
sudo tail -f /var/log/apache2/access.log
```

### Error Log
```bash
sudo tail -f /var/log/apache2/error.log
````

# Security and Permissions

### Check Configuration Syntax:
```bash
sudo apache2ctl configtest
```

### Set Permissions for Web Directory:
```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

These commands cover the basic operations you'll need to manage an Apache2 server on Ubuntu.
