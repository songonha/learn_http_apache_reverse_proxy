1/ New from backup and edit Public IP to new Droplet.

2/ Copy conf file for wss

3/ Rm old conf file.

4/ a2ensite new wss domain site conf

5/ Buy zerossl.com for wss.
  => Get openssl req -new -newkey ....
  
6/ Sudo =>

  sudo a2enmod ssl
  
  sudo a2enmod headers
  
  
/ Run server.

/ All done!!!
