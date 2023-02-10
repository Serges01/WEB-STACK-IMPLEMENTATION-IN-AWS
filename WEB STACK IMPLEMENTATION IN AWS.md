**WEB STACK IMPLEMENTATION IN AWS**

Basically a stack is just a way of keeping things in order one over the other. 

Therefore a technology stack keeps or it is a combination of several technologies stacked together in order to build an application. 

They are acronymns for individual technologies used together for a specific technology product. some examples are…

- LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)
- LEMP (Linux, Nginx, MySQL, PHP or Python, or Perl)
- MERN (MongoDB, ExpressJS, ReactJS, NodeJS)
- MEAN (MongoDB, ExpressJS, AngularJS, NodeJS

**Prerequisites**

In order to complete this project you will need an AWS account and a virtual server with Ubuntu Server OS.

After creating your AWS account, log in to reach the console home as seen below.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.001.png)

Click on the EC2 service in order to create an instance.


![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.002.png)

I have already created some instances. So to create one click on launch instance.


![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.003.png)

Give a name to your server.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.004.png)

Launch a new "EC2" instance of t2.micro family with Ubuntu Server 22.04 LTS(HVM) 64 bit

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.005.png)

You can use a key pair to securely connect to your instance. Ensure that you have access to the selected key pair before you launch the instance. 

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.006.png)


Click on Create new key pair then click on Create key pair.

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.007.png)

Configure Security Group; A security group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic. Inbound rules control the incoming traffic to your instance, and outbound rules control the outgoing traffic from your instance. When you launch an instance, you can specify one or more security groups.

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.008.png)

Click on create security group.

Under the Network settings, select existing security group.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.009.png)

Click on security groups to select the security groups to select the security group created.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.010.png)

Then click on launch instance.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.011.png)

Click on instance to see if the new created one is running.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.012.png)


Click on the running instance in order to see the instance details.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.013.png)


Next** is to connect my instance to an SSH Client by clicking on connect.

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.014.png)

**Connecting to EC2 terminal**

**Using the terminal on MAC/Linux**

- The terminal is already installed by default. You just need to open it up.
- You do not need to convert to a .ppk file. Just use the same key as downloaded from AWS.
- Change directory into the location where your PEM file is. Most likely will be in the Downloads folder

cd ~/Downloads

- Change premissions for the private key file (.pem), otherwise you can get an error "Bad permissions"

sudo chmod 0400 <private-key-name>.pem

- Connect to the instance by running

ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.015.png)

Answer yes to carry on

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.016.png)

Congratulations! You have just created your very first Linux Server in the Cloud and our set up looks like this now: (You are the client)


![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.017.png)
# **Step 1 — Installing Apache and Updating the Firewall**
- We need to Install Apache using Ubuntu’s package manager, apt:

$ sudo apt update

$ sudo apt install apache2

**To verify that apache2 is running as a Service in our OS, use following command**

`              `$ sudo systemctl status apache2

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.018.png)

If it is green and running, then you did everything correctly – you have just launched your first Web Server in the Clouds!

Before we can receive any traffic by our Web Server, we need to open TCP port 80 which is the default port that web browsers use to access web pages on the Internet

To open our port 80, i went back to the instance, clicked on security, clicked on edit inbound rules and i add rules. i added port 80 for http and port 443 https and i cliked on save rules

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.019.png)

Our server is running and we can access it locally and from the Internet (Source 0.0.0.0/0 means ‘from any IP address’).

First, let us try to check how we can access it locally in our Ubuntu shell, run:

curl http://localhost:80

or

` `curl <http://127.0.0.1:80>

Now it is time for us to test how our Apache HTTP server can respond to requests from the Internet. Open a web browser of your choice and try to access following url

[http://<Public-IP-Address>:80]()

Another way to retrieve your Public IP address, other than to check it in AWS Web console, is to use following command:

curl -s http://169.254.169.254/latest/meta-data/public-ipv4

If you see the following page, then your web server is now correctly installed and accessible through your firewall.

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.020.png)
# **STEP 2 — INSTALLING MYSQL**
Now that you have a web server up and running, you need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database. MySQL is a popular relational database management system used within PHP environments, so we will use it in our project.

Again, use ‘apt’ to acquire and install this software:

When prompted, confirm installation by typing Y, and then ENTER.

When the installation is finished, log in to the MySQL console by typing:

$ sudo mysql


This will connect to the MySQL server as the administrative database user root, which is inferred by the use of sudo when running this command. You should see output like this:

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.021.png)

It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql\_native\_password as default authentication method. We’re defining this user’s password as PassWord.1.

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql\_native\_password BY 'PassWord.1';


Exit the MySQL shell with:

mysql> exit

- After the installation it is recommended that we run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lockdown access to our database system.
- Start the interactive Script by running:

$ sudo mysql\_secure\_installation

Answer Y for yes, or anything else to continue without enabling.

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.022.png)
### For the rest of the questions, We press Y and hit the ENTER key at each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes we have made.
when you are done, you will get this **output:**

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.023.png)

- When you're finished, test if you're able to login to the MySQL Console by typing:

$ sudo mysql

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.024.png)

- To exit the MySQL Console, type: exit

mysql> exit


# **STEP 3 — INSTALLING PHP**
#
You have Apache installed to serve your content and MySQL installed to store and manage your data. PHP is the component of our setup that will process code to display dynamic content to the end user. In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need libapache2-mod-php to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.

To install these 3 packages at once, run:

$ sudo apt install php libapache2-mod-php php-mysql

Once the installation is finished, you can run the following command to confirm your PHP version:

$ php -v

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.025.png)

At this point, your LAMP stack is completely installed and fully operational.

We will configure our first Virtual Host in the next step.
## **Step 4 — Creating a Virtual Host for your Website using Apache**
In this project, you will set up a domain called projectlamp, but you can replace this with any domain of your choice.

Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory. We will leave this configuration as is and will add our own directory next next to the default one.

Create the directory for projectlamp using ‘mkdir’ command as follows:

$ sudo mkdir /var/www/projectlamp

Next, assign ownership of the directory with the $USER environment variable, which will reference your current user.

` `$ sudo chown -R $USER:$USER /var/www/projectlamp

- We can now open a new configuration file in Apache’s sites-available directory using our preferred command-line editor. Here, we’ll be using vi

This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.026.png)

You can use the ls command to show the new file in the sites-available directory

$ sudo ls /etc/apache2/sites-available

You will see something like this;

000-default.conf  default-ssl.conf  projectlamp.conf

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.027.png)

With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory. If you would like to test Apache without a domain name, you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.

You can now use a2ensite command to enable the new virtual host:

$ sudo a2ensite projectlamp

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.028.png)

You might want to disable the default website that comes installed with Apache. This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would overwrite your virtual host. To disable Apache’s default website use a2dissite command , type:

$ sudo a2dissite 000-default

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.029.png)

To make sure your configuration file doesn’t contain syntax errors, run:

$ sudo apache2ctl configtest

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.030.png)

Finally, reload Apache so these changes take effect:

$ sudo systemctl reload apache2

Your new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:

Type and run :

$ sudo vi /var/www/projectlamp/index.html

see my input:

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.031.png)

Now go to your browser and try to open your website URL using IP address:

[http://<public-ip-address>:80]()

or you can also browse using your public dns. the result is the same

[http://<Public-DNS-Name>:80]()

see my output :

![Une image contenant texte

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.032.png)

You can leave this file in place as a temporary landing page for your application until you set up an index.php file to replace it. Once you do that, remember to remove or rename the index.html file from your document root, as it would take precedence over an index.php file by default.

To check your Public IP from the Ubuntu shell, run :

$(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.033.png)

$(curl -s <http://169.254.169.254/latest/meta-data/public-ipv4>)

# **STEP 5 — ENABLE PHP ON THE WEBSITE**
With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.

In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

$ sudo vim /etc/apache2/mods-enabled/dir.conf

#Change this: #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm #To this: DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.html

After saving and closing the file, you will need to reload Apache so the changes take effect:

$ sudo systemctl reload apache2

Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server.

Now that you have a custom location to host your website’s files and folders, we’ll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

Create a new file named index.php inside your custom web root folder:

$ vim /var/www/projectlamp/index.php

This will open a blank file. Add the following text, which is valid PHP code, inside the file:

<?php

phpinfo();

![](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.034.png)

When you are finished, save and close the file, refresh the page and you will see a page similar to this:

![Une image contenant table

Description générée automatiquement](Aspose.Words.4e84a912-959a-419f-8601-03701382b622.035.png)

- This page provides information about your server from the perspective of PHP. It is useful for debugging and to ensure that your settings are being applied correctly.
- If you can see this page in your browser, then your PHP installation is working as expected.
- After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:
- sudo rm /var/www/projectlamp/index.php
























