# SSL

## open ssl

Output the Certificate authority of a certificate (redundant)

> openssl x509 -in /path/to/server.crt -noout -subject

Output more the information about a certificate

> openssl x509 -in /path/to/server.crt -noout -text

example of path

> /etc/ssl/certs/internal.crt

# Unable to configure RSA server private key

www.digicert.com/kb/ssl-support/apache-fix-common-ssl-errors.htm

If you see one of these errors it usually means that the private key that is being loaded in the VirtualHost section of your .conf file doesn't match the SSL Certificate being loaded in the same section.

To check if the two files match, run the following OpenSSL command on each of them:

    openssl x509 -noout -modulus -in your_domain_com.crt | openssl md5

    openssl rsa -noout -modulus -in your_domain_com.key | openssl md5


I think this was solved by replacing/updating the certs.

## PFX certificate

PFX internal key will use internal.key and internal.crt

It will be encrypted with a password of your choice.

> sudo openssl pkcs12 -export -out example.pfx -inkey internal,key -in internal.crt


If you already have a PFX and want to see the inside, use this:

> sudo openssl pkcs12 -info -in whatever.pfx -notes

## HTTPD

Error log of the httpd service

> /etc/httpd/logs/ssl_error_log