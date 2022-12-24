## Configuration Application with Apache Reverse Proxy, PHP, MariaDB, NodeJS.
### Websocket Wss:

With Droplet:

1/ Link IP: Droplet Public IP

2/ MariaDB: sql_mode =>
   sql_mode=NO_ZERO_IN_DATE,NO_ZERO_DATE,NO_ENGINE_SUBSTITUTION

3/ Sties-available: /etc/apache2/sites-available
   
4/ Sample Configuration:

### <VirtualHost *:443>

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

### </VirtualHost>


### <VirtualHost *:443>

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

### </VirtualHost>


===============================================================


### Additional ProxyPass Keywords

Normally, mod_proxy will canonicalise ProxyPassed URLs. But this may be incompatible with some backends, particularly those that make use of PATH_INFO. The optional nocanon keyword suppresses this and passes the URL path "raw" to the backend. Note that this keyword may affect the security of your backend, as it removes the normal limited protection against URL-based attacks provided by the proxy.

Normally, mod_proxy will include the query string when generating the SCRIPT_FILENAME environment variable. The optional noquery keyword (available in httpd 2.4.1 and later) prevents this.

The optional interpolate keyword, in combination with ProxyPassInterpolateEnv, causes the ProxyPass to interpolate environment variables, using the syntax ${VARNAME}. Note that many of the standard CGI-derived environment variables will not exist when this interpolation happens, so you may still have to resort to mod_rewrite for complex rules. Also note that interpolation is supported within the scheme/hostname/port portion of a URL only for variables that are available when the directive is parsed (like Define). Dynamic determination of those fields can be accomplished with mod_rewrite. The following example describes how to use mod_rewrite to dynamically set the scheme to http or https:

RewriteEngine On


RewriteCond "%{HTTPS}" =off

RewriteRule "." "-" [E=protocol:http]

RewriteCond "%{HTTPS}" =on

RewriteRule "." "-" [E=protocol:https]


RewriteRule "^/mirror/foo/(.*)" "%{ENV:protocol}://backend.example.com/$1" [P]

ProxyPassReverse  "/mirror/foo/" "http://backend.example.com/"

ProxyPassReverse  "/mirror/foo/" "https://backend.example.com/"

