# Apache-redirects
KodeKloud Task

### The Nautilus devops team got some requirements related to some Apache config changes. They need to setup some redirects for some URLs. There might be some more changes need to be done. Below you can find more details regarding that:



httpd is already installed on app server 3. Configure Apache to listen on port 3001.

Configure Apache to add some redirects as mentioned below:

a.) Redirect http://stapp03.stratos.xfusioncorp.com:<Port>/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/ i.e non www to www. This must be a permanent redirect i.e 301

b.) Redirect http://www.stapp03.stratos.xfusioncorp.com:<Port>/blog/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/news/. This must be a temporary redirect i.e 302.

#### Login to appserver and enter root account.
```
ssh bannner@stapp03


sudo su -
```
##### change apache listen to  port 3001
```
  vi /etc/httpd/conf/httpd.conf
```
#### Create main.conf to redirect.
```
vi /etc//httpd/conf.d/main.conf
```
##### configuration to redirect
```
<VirtualHost *:3001>
Severname stapp03.stratos.xfusioncorp.com
Redirect 301 / http://www.stapp03.startos.xfusioncorp.com:3001
</VirtualHost>
<VirtualHost *:3001>
Servername stapp03.stratos.xfusioncorp.com:<3001>/blog>
Redirect 302 /blog/  http://www.stapp03.stratos.xfusioncorp.com:<3001>/news/
</VirtualHost>
```
##### Restart the apache server
```
systemctl restart httpd
sytermctl status httpd
```
##### Validate using curl.
```
curl http://www.stapp03.startos.xfusioncorp.com:3001
```
