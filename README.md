# How to set SSL in your xampp server

### STEP-1:
Go to your **xampp** directory\
Find out the path **"G:\xampp\apache\crt"**

### STEP-2:
Copy **"makecert"** & **"cert.conf"** files over there (xampp\apache\crt)\
**"makecert"** & **"cert.conf"** file you will get from this repo\
also a .zip available, extract and get the batch file - **"makecert"**

### STEP-3:
Now open the file - **"cert.conf"** and edit below fields -
1) **commonName_default** = YOUR_SITE_NAME (ex:onexcrm.local)
2) **emailAddress_default** = YOUR_EMAIL_ADDRESS (ex:abc@gmail.com)
3) **DNS.1** = YOUR_SITE_NAME (ex:onexcrm.local) (same with above)\
   and save the file

### STEP-4:
Now run the batch file - **"makecert"**, just click on it\
It will ask few things, just fill-up\
When it done then a folder of your site name will be created into the "apache\crt" directory\
With this new folder 2 files will be available
1) **server** (certificate file)
2) **server.key** (certificate key file)

### STEP-5:
Now need to install the certificate file\
click on it and install it

### STEP-6:
Now go to your **"httpd-vhosts.conf"** file\
ex: G:\xampp\apache\conf\extra\httpd-vhosts.conf\
and set the domain with below code snippets\
once done, save the "httpd-vhosts.conf" file and restart your xampp

```
<VirtualHost your-site.local:80>
    DocumentRoot "D:/xampp/htdocs/project-folder/public"
    ServerName your-site.local
    <FilesMatch "\.(cgi|shtml|phtml|php)$">
        #SSLOptions +StdEnvVars
    </FilesMatch>
    <Directory "D:/xampp/htdocs/project-folder/public">
        Order deny,allow
        Allow from all
        Require all granted
        #SSLOptions +StdEnvVars
    </Directory>
</VirtualHost>
<VirtualHost your-site.local:443>
    DocumentRoot "D:/xampp/htdocs/project-folder/public"
    ServerName your-site.local
    <FilesMatch "\.(cgi|shtml|phtml|php)$">
        SSLOptions +StdEnvVars
    </FilesMatch>
    <Directory "D:/xampp/htdocs/project-folder/public">
        Order deny,allow
        Allow from all
        Require all granted
        SSLOptions +StdEnvVars
    </Directory>
    SSLEngine on
	SSLCertificateFile "crt/your-site.local/server.crt"
	SSLCertificateKeyFile "crt/your-site.local/server.key"
</VirtualHost>
```
### STEP-7:
Now go to "C:\Windows\System32\drivers\etc\" this path and open **'hosts'** file\
and set your domain with the local ip, like -\
```
127.0.0.1  your-site.local
```

### STEP-8:
Now open your site in browser\
your-site.local \
http://your-site.local \
https://your-site.local \
all will work!

### Done!!!
