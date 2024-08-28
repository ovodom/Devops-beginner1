#**Setup a Static Website Using Nginx**

## Introduction: This project is deals with installing Nginx, Downloading a free HTML website files, creating an elastic IP address, validating the website using the IP address and validating the website SSL usingSSL utility.
Breakdown steps:
1.	On the console home I clicked on EC2, clicked on launch instance. I was able to access Launch Instant page.
2.	Under name, I entered p1. I chose Ubuntu. SSH, HTTP and HTTPS access.
3.	I clicked launch instance to launch instance.
4.	Clicked on connect, copied command on SSH client.
5.	Opened a terminal on my .pem file, okay.pem was was downloaded. I pasted the SSH command and pressed enter key
6.	I created an elastic IP and got it associated.
7.	Again I entered the command copied from SSH client, pasted it on terminal and clicked enter.
8.	My IP address, 34.198.162.153 pasted on web browser to confirm Nginx setup. This showed welcome to Nginx to confirm it. 
9.	I visited tooplate.com to download a free HTML website file.
10.	sudo nano /etc/nginx/sites-available/default pasted on terminal and root directory edited.
11.	IP address copied and pasted on a browser. It showed the free HTML page.
12.	I visited my domain and made some changes.
13.	Domain name entered on route 53 (AWS)
14.	R




