# How to set SSL in your xampp server



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
