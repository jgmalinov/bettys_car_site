## Get Apache to serve your website locally 
#### (loopback on the same machine / other devices in the LAN)


### Installing Apache

1. Open your terminal
2. Type in the following commands:
            
            > sudo apt update

            > sudo apt install apache2
### Cloning this repo 
1. Navigate to the folder where apache will look for your code:

            > cd /var/www

2. Make a directory, enter it and initialize it as a local Git repo:

            > sudo mkdir car-website
         
            > cd car-website

3. Clone this repository:

            > git clone https://github.com/jgmalinov/bettys_car_site.git

### Configure a virtual host
1. Figure out and write down your local IP address:
            
            > hostname -I | awk '{print $1}'

2. Go back to the root folder and then:

            > cd /etc/apache2/sites-available/

3. Copy the default VirtualHost and use it as a template for yours. Open the newly copied file for editing:

            > sudo cp 000-default.conf car-website.conf
         
            > nano car-website.conf
            

4. Edit the file as follows:

<img width="974" alt="image" src="https://github.com/jgmalinov/bettys_car_site/assets/99488455/ae5b48aa-3a73-49f1-b1e9-c14156532213">

            > CTRL + X
            
            > CTRL + Y
            
            > ENTER

5. Enable local domain name resolution so that you can access your website from a custom domain when looping back (request from same device)
            
            >  nano ../../hosts (full address -> /etc/hosts)
             
            >  set up the domain name to resolve to your local IP:
               
<img width="538" alt="image" src="https://github.com/jgmalinov/bettys_car_site/assets/99488455/22e83784-41ab-4ddf-9abc-3d5d2922df84">

### Activate Virtual Host and restart server

            > a2ensite car-website.conf
            
            > systemctl restart apache2.service
            

### Test out your website!
            > From the browser -> e.g. http://bettys-car-website.com or with local IP: http://172.31.4.252/
            
            > From the terminal -> curl http://bettys-car-website.com or with local IP: curl http://172.31.4.252/
            

- Using http://localhost should take you to Apache's default page and not yours
- Try out reaching the website from other machines in the same LAN but only via the local IP
