# Setup Multiple Static Websites on a Single Server Using Nginx Virtual Hosts

In this project, we will learn the concept of subdomains and hosting multiple websites on a single server using Nginx Virtual Host configuration.

## Key Concepts Covered

- AWS (EC2 and Route 53)
- EC2
- Linux(Ubuntu)
- Nginx
- DNS
- Subdomains
- SSL (certbot)
- OpenSSL command

## Project Tasks

<table>
<tr>
<td width="20%">S/N</td>
<td width="80%">Project Tasks</td>
</tr>
<tr>
<td>1</td>
<td>Install and configure Nginx on a server</td>
</tr>
<tr>
<td>2</td>
<td>Create two website directories with two different website templates.</td>
</tr>
<tr>
<td>3</td>
<td>Create two subdomains</td>
</tr>
<tr>
<td>4</td>
<td>Add the IP of the server as A record to the two subdomains.</td>
</tr>
<tr>
<td>5</td>
<td>Configure the Virtual host to point two subdomains to two different website directories.</td>
</tr>
<tr>
<td>6</td>
<td>Validate the setup by accessing the subdomains.</td>
</tr>
<tr>
<td>7</td>
<td>Create a certbot SSL certificate for the root Domain.</td>
</tr>
<tr>
<td>8</td>
<td>Configure certbot on Nginx for two websites.</td>
</tr>
<tr>
<td>9</td>
<td>Validate the subdomain websites’ SSL using OpenSSL utility.</td>
</tr>
</table>

## Checklist

- [x] _Task 1_: Spin up a Ubuntu server & assign an elastic IP to it.
- [x] _Task 2_: SSH into the server and install and configure Nignx on a server.
- [x] _Task 3_: Create two website directories with two different website templates.
- [x] _Task 4_: Create two subdomains
- [x] _Task 5_: Add the IP of the server as A record to the two subdomains.
- [x] _Task 6_: Configure the Virtual host to point two subdomains to two different website directories.
- [x] _Task 7_: Validate the setup by accessing the subdomains.
- [x] _Task 8_: Create a certbot SSL certificate for the root Domain.
- [x] _Task 9_: Configure certbot on Nginx for the two websites.
- [x] _Task 10_: Validate the subdomain websites’ SSL using OpenSSL utility.

## Documentation

<strong> Spin up a Ubuntu server & assign an elastic IP to it. </strong>

![ubuntu ec2 instance](image.png)
![assign elastic ip](image-1.png)

<strong>SSH into the server and install and configure Nignx on a server.</strong>

- run
  `sudo apt update` `sudo apt upgrade` `sudo apt install nginx`
- Start your Nginx server by running the `sudo systemctl start nginx` command, enable it to start on boot by executing sudo `systemctl enable nginx`, and then confirm if it's running with the `sudo systemctl status nginx` command.

  ![nginx confirmation page](image-2.png)

- Download your website template from your preferred website by navigating to the website, locating the template you want.

![download website template](image-3.png)

- Install unzip `sudo apt install unzip`
- run `sudo curl -o /var/www/html/2096_individual.zip https://www.tooplate.com/zip-templates/2096_individual.zip && sudo unzip -d /var/www/html/ /var/www/html/2096_individual.zip && sudo rm -f /var/www/html/2096_individual.zip `
  ![unzipped website template](image-4.png)

- Download the 2nd website template by running the following command:
  `sudo curl -o /var/www/html/2094_mason.zip https://www.tooplate.com/zip-templates/2094_mason.zip && sudo unzip -d /var/www/html/ /var/www/html/2094_mason.zip && sudo rm -f /var/www/html/2094_mason.zip`

![second website download being listed](image-5.png)
