<u>

# Setup WordPress Website Using LAMP Stack

</u>

Setting up a WordPress website using the LAMP stack (Linux, Apache, MySQL, PHP) is a powerful way to create a robust and scalable web presence. This project will guide you through each step of the process, from setting up your server environment to installing WordPress and configuring it for optimal performance. Whether you're a seasoned developer or a beginner, this tutorial will provide you with the knowledge and skills needed to deploy a fully functional WordPress site. By the end of this guide, you'll have a solid understanding of how to leverage the LAMP stack to build and manage your own WordPress website, ensuring a secure, efficient, and customizable platform for your content.

<strong>Key Features:</strong>

- Step-by-step instructions for installing and configuring LAMP components.
- Secure database creation for your WordPress website.
- User-friendly guide for completing the WordPress installation process.

<strong>Benefits:</strong>

- Gain independence by managing your own WordPress website.
- Understand the core technologies behind WordPress.
- Customize your website to your exact needs.
- Embrace the flexibility and power of WordPress.

<table>

<tr>
<td width="20%">S/N</td>
<td width="80%">Project Tasks</td>
</tr>
<tr>
<td>1</td>
<td>Deploy an Ubuntu Server</td>
</tr>
<tr>
<td>2</td>
<td>Set up your LAMP stack on the server</td>
</tr>
<tr>
<td>3</td>
<td>Configure the wordpress Application</td>
</tr>
<tr>
<td>4</td>
<td>Map the IP address to the DNS A record</td>
</tr>
<tr>
<td>5</td>
<td>Validate the WordPress website setup by accessing the web address.</td>
</tr>
</table>

<u>

## Key Concepts Covered

</u>

- AWS (EC2 and Route 53)
- Linux(Ubuntu)
- Apache
- MySQL
- PHP
- Wordpress
- DNS
- SSL (certbot)
- OpenSSL command

<u>

## Documentation

</u>
- Create an EC2 ubuntu instance
- We will set an inbound rule for MYSQL in your security group by clicking on security and selecting the Security group.

_Pic1 goes here_

- Edit inbound rules

_Pic2 goes here_

- Add rule

_Pic 3 goes here_

- Click on Custom TCP and select MySQL/Aurora.

_Pic 4 goes here_

- Enter the IP address you want to allow access and click Save rules.

_Pic 5 goes here_

- SSH into your ubuntu server via your terminal.

_Pic 6 goes here_

---

## Install Apache

run `sudo apt update`

_Pic 7 goes here_

run `sudo apt install apache2`

_Pic 8 goes here_

- Enable Apache to start on boot by executing `sudo systemctl enable apache2` then verify its status with the `sudo systemctl status apache2` command

_Pic 9 goes here_

- Check if our server is running and accessible both locally and from the Internet by executing the following command: `curl http://localhost:80`

_Pic 10 goes here_

- Paste your instance IPv4 address into your broswer address bar and if installation was successful you should see the below page

_Pic 11 goes here_

## Install MYSQL

- run the command sudo apt install mysql-server

_Pic 12 goes here_

- Log in to the MySQL console by typing: `sudo mysql`

> [!NOTE]
> It's recommended that you run a security script included with MySQL to enhance security. Before running the script, set a password for the root user using the default authentication method mysql_native_password. For this project, we'll define the password as "pass", but you can choose any password you prefer.

- Run the following command to set the password for the root user with the MySQL native password authentication method: `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'pass';`. Exit the MySQL shell when you're done by typing `exit`.

_Pic 13 goes here_

- Start the interactive script by running: `sudo mysql_secure_installation`. Answer y for yes, or any other key to continue without enabling specific options.

- Set your password validation policy level.

_Pic 14 goes here_

> [!NOTE]
> set my password validation policy level to 0 because I don't require much security, as I will be terminating all resources immediately after this project. However, on the job, it's advised to use the strongest level, which is 2.

- Enable MySQL to start on boot by executing `sudo systemctl enable mysql` then confirm its status with the `sudo systemctl status mysql` command.

_Pic 15 goes here_

---

## Install PHP

Install PHP along with required extensions by running the following script: `sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip`

_Pic 16 goes here_

`sudo apt install php libapache2-mod-php php-mysql`

_Pic 17 goes here_

- Check what version of PHP you have installed by running `php -v`

_Pic 18 goes here_

<strong>Creating A Virtual Host For Your Website Using Apache</strong>

- Create the directory for Projectlamp using the 'mkdir' command as follows: `sudo mkdir /var/www/projectlamp` and assign ownership of the directory to our current system user using: `sudo chown -R $USER:$USER /var/www/projectlamp`

_Pic 19 goes here_

- Create and open a new configuration file in Apache's sites-available directory using your preferred command-line editor: `sudo vi /etc/apache2/sites-available/projectlamp.conf`

_Pic 20 goes here_

- Save your changes by pressing the `Es`c key, then type `:wq` and press `Enter`.

- Run the ls command `sudo ls /etc/apache2/sites-available` to show the new file in the sites-available directory

_Pic 21 goes here_

- Running `sudo a2ensite projectlamp` will enable the new virtual host using the a2ensite command

_Pic 22 goes here_

- To disable Apache's default website, use the a2dissite command. Type: `sudo a2dissite 000-default`

- To ensure your configuration file doesn’t contain syntax errors, run: `sudo apache2ctl configtest`. You should see "Syntax OK" in the output if your configuration is correct.

_Pic 23 goes here_

- Reload Apache for the changes to take effect by running `sudo systemctl reload apache2`

- To create the index.html file with the content "Hello LAMP from Etubom" in the /var/www/projectlamp directory, use the following command: `sudo echo 'Hello LAMP from Etubom's computer' > /var/www/projectlamp/index.html`

_Pic 24 goes here_

- Go back to your browser and refresh your IPv4 public address to see if your changes come through

_Pic 25 goes here_

- Remove the index.html file by running the following command: `sudo rm /var/www/projectlamp/index.html`

<strong>Enable PHP On The Website</strong>
With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To change the precedence of index files (such as index.php over index.html) in Apache, you'll need to edit the dir.conf file. Here’s how you can do it:
