## Configuration Application with Apache Reverse Proxy, PHP, MariaDB, NodeJS.
### Websocket Wss:

With Droplet:

1/ Link IP: Droplet Public IP

2/ MariaDB: sql_mode =>
   sql_mode=NO_ZERO_IN_DATE,NO_ZERO_DATE,NO_ENGINE_SUBSTITUTION

3/ Sties-available: /etc/apache2/sites-available
   
4/ Sample Configuration:

<VirtualHost *:443>
    ServerName redmine.DOMAIN.com
    
    SSLEngine On
    
    SSLProxyEngine On
    
    ProxyRequests Off
    
    ProxyPreserveHost On
    
    SSLCertificateFile /etc/apachekeys/redmine.DOMAIN.com.crt
    
    SSLCertificateKeyFile /etc/apachekeys/DOMAIN.com.key
    
    SSLCertificateChainFile /etc/apachekeys/sub.class1.server.ca.pem
    
    SSLCACertificateFile /etc/apachekeys/ca.pem
    
    ProxyHTMLInterp On
    
    ProxyHTMLExtended On
    
    ProxyHTMLURLMap (.*)192.168.1.14(.*) https://redmine.DOMAIN.com$2 [Rin]
    
    ProxyPass / https://192.168.1.14/
    
    ProxyPassReverse / https://192.168.1.14/

</VirtualHost>


<VirtualHost *:443>

ServerName sharepoint.DOMAIN.com

   SSLEngine On
   
   SSLProxyEngine On
   
   ProxyRequests Off
   
   SSLCertificateFile /etc/apachekeys/sharepoint.DOMAIN.com.crt
   
   SSLCertificateKeyFile /etc/apachekeys/DOMAIN.com.key
   
   SSLCertificateChainFile /etc/apachekeys/sub.class1.server.ca.pem
   
   SSLCACertificateFile /etc/apachekeys/ca.pem
   
   SetOutputFilter INFLATE;proxy-html;DEFLATE;
   
   ProxyHTMLInterp On
   
   ProxyHTMLExtended On
   
   ProxyHTMLURLMap (.*)192.168.1.11(.*) https://sharepoint.DOMAIN.com$2 [Rin]
   
   ProxyPass / http://192.168.1.11/
   
   ProxyPassReverse / http://192.168.1.11/

</VirtualHost>
