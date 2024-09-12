# Lamp-Webstack

# Setting up a LAMP Stack on an Amazon EC2 Instance

In the realm of web development, having a robust and efficient environment is paramount. The LAMP stack, which stands for **Linux, Apache, MySQL, and PHP**, has been a cornerstone for countless web applications and dynamic websites. In this comprehensive guide, we'll delve into the intricacies of setting up a LAMP stack on an Amazon EC2 instance, empowering you to create, deploy, and host your web applications with ease.

## Understanding the Components

Before we dive into the setup process, let's briefly understand the components of the LAMP stack:

- **Linux**: Ubuntu Server 22.04 LTS serves as our operating system.
- **Apache**: Apache HTTP Server acts as the web server.
- **MySQL**: MySQL Database Server manages our relational databases.
- **PHP**: PHP, the Hypertext Preprocessor, handles server-side scripting.

## Setting up the EC2 Instance

### 1. Launch an EC2 Instance
- Sign in to the **AWS Management Console**.
- Navigate to the **EC2 Dashboard** and click on "Launch Instance."
- Select **Ubuntu Server 22.04 LTS** as the operating system.

### 2. Configure Instance Details
- Customize the instance type, network, subnet, and other settings according to your requirements.

### 3. Add Storage
- Allocate storage space based on your application needs.

### 4. Add Tags
- Optionally, enhance organization by adding tags to your instance.

### 5. Configure Security Group
- Establish a security group, allowing inbound traffic on ports:
  - **80** (HTTP)
  - **22** (SSH)
  - **443** (HTTPS)
  - Make sure to limit SSH access to your IP address for security.

### 6. Review and Launch
- Review your configuration and proceed with launching the instance.

### 7. Connect to the Instance
- Use ``` ssh -i path/to/key pair ubuntu@public address```

## Installing the LAMP Stack

### 1. Update Package Repository
```sudo apt update ```

### 2. Install Apache
```sudo apt install apache2```

### 3. Enable and Verify Apache
Enable Apache to start at boot:
```sudo systemctl enable apache2```

Check the status of Apache to ensure it’s running:
```sudo systemctl status apache2```

### 4. Test Apache Installation
Access Apache by visiting:
```http://localhost:80``` or
```http://127.0.0.1:80``` on your browser

### 5. Install MySQL
Install MySQL Server:
```sudo apt install mysql-server```

Secure the MySQL installation:
```sudo mysql_secure_installation```

### 6. Install PHP
Install PHP and necessary modules:
```sudo apt install php libapache2-mod-php php-mysql```

## Creating a Virtual Host with Apache

### 1. Set Up Domain Name
Create a directory for your project under /var/www/:
```sudo mkdir /var/www/projectlamb```

change ownership
```sudo chown -R $USER:$USER /var/www/projectlamb```

### 2. Configuration with Apache
Create a new virtual host configuration file in Apache's sites-available directory:
```sudo nano /etc/apache2/sites-available/projectlamb.conf```

Add the following configuration:
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName projectlamb
    ServerAlias www.projectlamb
    DocumentRoot /var/www/projectlamb
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### 3. Enable Virtual Host
Enable your newly created virtual host:
```sudo a2ensite projectlamb```

Disable the default Apache configuration:
```sudo a2dissite 000-default```

#### 4. Reload Apache
Ensure changes take effect:
```sudo systemctl reload apache2```

#### 5. Testing
Create an index.html file in your project directory:

```echo "<h1>This is Kenneth</h1>" > /var/www/projectlamb/index.html```

Access the website via the browser at ```http://<public-ip-address>:80```

## Enabling PHP on the Website
### 1. Modify Directory Index
Adjust Apache’s configuration to prioritize PHP files:

```sudo vi /etc/apache2/mods-enabled/dir.conf```

Move index.php to the first position:
```
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule> 
```

### 2. Reload Apache
Apply the changes:
```sudo systemctl reload apache2```

### 3. Create PHP Test Script
Create a simple PHP script to verify the installation:
```echo "<?php phpinfo(); ?>" > /var/www/projectlamp/index.php```

### 4. Test PHP Installation
Refresh your page and verify that PHP is working

## Conclusion

Setting up a LAMP stack on an AWS EC2 instance was an invaluable hands-on experience that deepened my understanding of web hosting and server management. By configuring Linux, Apache, MySQL, and PHP from scratch, I gained practical skills in deploying scalable web applications. This project provided a solid foundation for future work in DevOps and web development, as I now have the ability to set up reliable environments for dynamic websites.

Moving forward, these skills will be essential in more complex projects, particularly in cloud environments where scalability and performance are key. I’m excited to apply what I’ve learned here to future projects and continue refining my expertise in managing server infrastructures.
