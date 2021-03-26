# Linux misc.

avoid timeout

> export TMOUT=0

Elevate to root

> sudo su -

## See the firewall open ports (rhel)

> sudo firewall-cmd --list-ports

## See active ports

> netstat -tulpn | egrep "80|443|4503" | grep LISTEN

## Tunnel a port through ssh.

> ssh -L 4503:localhost:4503 user@hostname

Now what should be exposed in the port of the remote hostname will be available in your local computer

Now you can go into your local computer and enter this in a browser.

*http://localhost:4503*

---

AEM ports: 

http:4503, https: 8443

## register a hostname only for you

open */etc/hosts* with sudo

insert a new line of

        #IP-address hostname
        10.45.313.2 hello.com.net