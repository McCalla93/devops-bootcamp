## PROJECT TITLE : Setup Load Balancing for Static Website Using Nignx

1. I spinned up my 3 ubuntu servers. and i clearly named them to avoid mistakes
![alt text](<.vscode/img/DEPLOY 3servers.png>)

2. I installed Nginx and Setup my Website
3. I downloaded my website template from my preferred website and navigated to the website, locating the template i want.

4. I right clicked and selected Inspect from the drop down menu.



5. I clicked on the Network tab.


6. I clicked the download button and right clicked on the website name.


7. I Selected Copy and clicked on Copy URL.


8. To install Nginx i executed the following commands.

sudo apt update

sudo apt upgrade

sudo apt install nginx

9. I started my Nginx server by running the sudo systemctl start nginx command, I enabled it to start on boot by executing sudo systemctl enable nginx, and then i confirmed if it's running with the sudo systemctl status nginx command.


## I visited my instances IP address in a web browser to view my default Nginx startup page.

10. I executed sudo apt install unzip to install the unzip tool and run the following command to download and unzip your website files sudo curl -o /var/www/html/2135_mini_finance.zip https://www.tooplate.com/zip-templates/2135_mini_finance.zip && sudo unzip -d /var/www/html/ /var/www/html/2135_mini_finance.zip && sudo rm -f /var/www/html/2135_mini_finance.zip.

![alt text](<.vscode/img/sudo curl.png>)
11. To set up my website's configuration, i created a new file in the Nginx sites-available directory. I Used the following command to open a blank file in a text editor: sudo nano /etc/nginx/sites-available/finance.

## I copied and pasted the following code into the open text editor.

server {
    
    listen 80;
    server_name example.com www.example.com;

    root /var/www/html/2135_mini_finance;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

12. I edited the root directive within my server block to point to the directory where my downloaded website content is stored.

13. Created a symbolic link for both websites by running the following command. sudo ln -s /etc/nginx/sites-available/finance /etc/nginx/sites-enabled/

14. I ran the sudo nginx -t command to check the syntax of the Nginx configuration file, and when successful i then ran the sudo systemctl restart nginx command.

## I Repeated the process for the second website also.
15. I executed sudo apt install unzip to install the unzip tool and i  ran the following command to download and unzip my website files sudo curl -o /var/www/html/2133_moso_interior.zip https://www.tooplate.com/zip-templates/2133_moso_interior.zip && sudo unzip -d /var/www/html/ /var/www/html/2133_moso_interior.zip && sudo rm -f /var/www/html/2133_moso_interior.zip.

To set up my website's configuration, i created a new file in the Nginx sites-available directory. I Used the following command to open a blank file in a text editor: sudo nano /etc/nginx/sites-available/interior.

## I copied and pasted the following code into the open text editor.

server {
    
    listen 80;
    server_name example.com www.example.com;

    root /var/www/html/2133_moso_interior;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

16. I edited the root directive within my server block to point to the directory where my downloaded website content is stored.

17. Created a symbolic link for both websites by running the following command. sudo ln -s /etc/nginx/sites-available/finance /etc/nginx/sites-enabled/

18. I ran the sudo nginx -t command to check the syntax of the Nginx configuration file, and when successful i then ran the sudo systemctl restart nginx command.

### On my first server, I ran sudo rm /etc/nginx/sites-enabled/default, and on my second server, I ran sudo rm /etc/nginx/sites-enabled/default. This will delete the default site-enabled folders and enable Nginx to serve content from my specified website directories. To avoid seeing the default Nginx page, the default folders has to be deleted.

19. I ran the sudo systemctl restart nginx command to restart my server.

20. I checked both IP addresses to confirm my website is up and running.

![alt text](<.vscode/img/finance Not sec p3.png>)

![alt text](<.vscode/img/moso interior Not Sec p3.png>)


### I Configured my Load balancer by:
21. Installing Nginx on the server i want to use as a load balancer, and i executed sudo systemctl status nginx to ensure it's running.


22. I executed sudo nano /etc/nginx/nginx.conf to edit my Nginx configuration file.


#### I added the following within the http block.

    upstream kolawolemccalla {
    server 3.229.211.56;
    server 54.144.213.184;
    # Add more servers as needed
}

server {
    listen 80;
    server_name kolawolemccalla.space www.kolawolemccalla.space;

    location / {
        proxy_pass http://kolawolemccalla;
    }
}


![alt text](<.vscode/img/sudo nano p3.png>)

23. I replaced the necessary placeholders as shown in the picture above. Substitute 3.229.211.56 and 54.144.213.184, I also replaced <your domain> www.<your domain> with your root domain and subdomain name <kolawolemccalla.space> www.<kolawolemccalla.space> and I updated proxy_pass and the other relevant fields accordingly.

24. I ran sudo nginx -t to check for syntax error.


25. I then applied the changes by restarting Nginx: sudo systemctl restart nginx

## I Created An A Record


26. After creating an A Record i then went to the terminal i used in setting up my first website and ran sudo nano /etc/nginx/sites-available/finance to edit my settings. I entered the name of my domain and then saved my settings.


27. I restarted my nginx server by running the sudo systemctl restart nginx command.

28. I went back to the terminal i used in setting my second website and ran sudo nano /etc/nginx/sites-available/interior to edit my settings. I entered the name of my domain and then saved my settings.


29. I restarted my nginx server by running the sudo systemctl restart nginx command.


I went back to my domain name in a web browser to verify that my website is accessible.
![alt text](<.vscode/img/kol.space finance.png>)

I reloaded the webpage to ensure the load balancer distributes traffic evenly between my servers.
![alt text](<.vscode/img/Kol.space moso.png>)


## To Install certbot and Request For an SSL/TLS Certificate:

30. I installed certbot by executing the following commands: sudo apt update sudo apt install python3-certbot-nginx
![alt text](<.vscode/img/certbot SSL 1.png>)
31. I executed the sudo certbot --nginx command to request my certificate.

32. I got a congratulatory message that says https has been successfully enabled.
![alt text](<.vscode/img/Congratulatory mess.png>)

33. I then accessed my website to verify that Certbot has successfully enabled HTTPS.
https enabled
![alt text](<.vscode/img/finance SEC.png>)
![alt text](<.vscode/img/moso SEC.png>)
34. It was also recommended to renew my LetsEncrypt certificate at least every 60 days or more frequently. I tested the renewal command in dry-run mode: sudo certbot renew --dry-run
![alt text](<.vscode/img/Screenshot (64).png>)

The End Of Project 3