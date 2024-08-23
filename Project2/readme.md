# PROJECT TITLE : To Setup a Static Website Using Nginx
The goal of the project is to have a fully deployed and secure static website ready !

In this project, I will be:
Building with Nginx: I'll set up Nginx as my web server, the engine that delivers my website content to the world.

Connecting with Route53: I'll configure Amazon Route53, the DNS service that directs visitors to your website's location.

Securing with Certbot: I'll implement HTTPS encryption using Certbot, ensuring a safe and secure connection for your website.

By the end of this project, I'll have a fully deployed and secure static website

## Below are the respective task for Project 1
S/N	Project Tasks

1	Buy a domain name from a domain Registrar

2	Spin up an Ubuntu server & assign an elastic IP to it

3	SSH into the server and install Nginx

4	Download freely HTML website files(too plate) or use your personal code

5	Copy the website files to the Nginx website directory

6	Validate the website using the server IP address

7	In Route53, create an A record and add the Elastic IP

8	Using DNS verify the website setup

9	Install certbot and Request For an SSL/TLS Certificate

10	Validate the website SSL using the OpenSSL utility


## Documentation
I Created An Ubuntu Server
And i clicked on EC2 within the AWS management console.
1
![alt text](.vscode/img/EC2.png)
I clicked on Launch Instance
2
![alt text](<.vscode/img/launch instance.png>)
I named my instance and selected the Ubuntu AMI.
3
![alt text](.vscode/img/ubuntu.png)
I clicked the create new key pair button to generate a key pair for secure connection to my instance.
4

I enter a Key pair name and click on Create key pair.
5

I Enabled SSH, HTTP, and HTTPS access, then i proceeded to click Launch instance.
6

I Clicked on the created instance.
7
![alt text](<.vscode/img/created intance.png>)

I Clicked on the Connect button.
8
![alt text](<.vscode/img/connect button.png>)
I Copied the command provided under SSH client.
9
![alt text](<.vscode/img/connect to instance.png>)
I Opened a terminal in the directory where my .pem file was downloaded, i paste the command and press Enter.

 

I Clicked on the Allocate Elastic IP address button.
![alt text](<.vscode/img/allocate elastic ip add.png>)

I Kept the settings unchanged and proceeded to click Allocate.

I Associated my Elastic IP address with my running instance.

I Selected the instance i wish to associate with the elastic IP address, then i click on Associate.


i Pasted the command into my terminal and then i pressed Enter. When prompted, i typed "yes" and press Enter to connect.

i Installed Nginx and Setup My Website
i used the following commands.
sudo apt update

sudo apt upgrade

sudo apt install nginx

i started my Nginx server by running the sudo systemctl start nginx command, i enabled it to start on boot by executing sudo systemctl enable nginx, and then i confirmed if it's running with the sudo systemctl status nginx command.

I went back to my EC2 dashboard and copy my Public IPv4 address.


i visited my instances Public IPv4 address in a web browser to view the default Nginx startup page.

![alt text](<.vscode/img/ip address not secured.png>)


I Got my template from Tooplate and selected the website template i prefer.


I Ran this command sudo curl -o /var/www/html/2134_gotto_job.zip https://www.tooplate.com/zip-templates/2134_gotto_job.zip to download the websites file to my html directory.


To install the unzip tool, i ran the following command: sudo apt install unzip.

i navigated to the web server directory by running the following command: cd /var/www/html.

i unzipped the contents of my website by running sudo unzip <2134_gotto_job.zip>


i updated my nginx configuration by running the command sudo nano /etc/nginx/sites-available/default. Then, edited the root directive within my server block to point to the directory where my downloaded website content is stored.

I restarted Nginx to apply the changes by running: sudo systemctl restart nginx.

i Opened a web browser and went to my Public IPv4 address/Elastic IP address to confirm that my website is working as expected.

I create An A Record
To make my website accessible via my domain name rather than the IP address, i will need to set up a DNS record. I did this by buying my domain from Domain.com and then moving hosting to AWS Route 53, where I set up an A record.

i went back to my AWS console, searched for Route 53, and then choose Route 53.

i clicked on Get started.
![alt text](<.vscode/img/click on get started.png>)

i Selected Create hosted zones and i clicked on Get started.


I entered my Domain name, choose Public hosted zone and then click on Create hosted zone.
![alt text](<.vscode/img/enter domain name and create hosted zone.png>)


i Selected the created hosted zone and copied the assigned Values.


i went back to my domain registrar and selected Custom DNS within the NAMESERVERS section.

i then Pasted the values i copied from Route 53 into the appropriate fields, then i clicked the checkmark symbol to save the changes.
![alt text](<.vscode/img/paste values from route 53.png>)

i went back to my AWS console and clicked on Create record.


i Pasted my Elastic IP address and then clicked on Create records.and my A record has been successfully created.


i Clicked on create record again, to create the record for my sub domain.

I inputed the Record name(www), pasted my IP address, and then click on Create records.

i opened my terminal and ran sudo nano /etc/nginx/sites-available/default to edit my settings. I entered my domain and subdomain names, then save the changes.
34

I restarted my nginx server by running the sudo systemctl restart nginx command.

I went to my domain name in a web browser to verify that my website is accessible.
![alt text](<.vscode/img/not secured.png>)
The picture above was before i corrected my domain name 

I installed certbot by executing the following commands: sudo apt update sudo apt install certbot python3-certbot-nginx


I Executed the sudo certbot --nginx command to request my certificate. i also followed the instructions provided by certbot and selected the domain name i would like to activate HTTPS.


i Verified the website's SSL using the OpenSSL utility with the command: openssl s_client -connect kolawolemccalla.space:443


I Visited https://<kolawolemccalla.space> to view my website.
![](<.vscode/img/Screenshot (17).png>)
The End Of Project 1