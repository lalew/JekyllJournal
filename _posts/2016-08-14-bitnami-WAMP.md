---
layout: post
title: Bitnami/WAMP
date:   2016-08-14
tags: [bitnami, setup, WAMP]
---
Bitnami - Easy stack setup. Inside contains common adjustments needed to relate Bitnami files to typical WAMP files.
<!--more-->

# Default WAMP Setup  

The username is 'root' for phpMyAdmin and 'postgres' for phpPgAdmin, and the password is the one specified by you during the installation process.

Inside apache/bin
{% highlight shell %}
httpd
//Add OR Remove from list of running services
httpd -k install
net start apache2.4
net stop apache2.4
httpd -k uninstall
{% endhighlight %}

Adding PHP to apache
{% highlight php %}
//Place at end of C:\apache\conf\httpd.conf
LoadModule php5_module "C:/php/php5apache2_4.dll"
AddHandler application/x-httpd-php .php
PHPIniDir "c:/php"
{% endhighlight %}

PHP Test Script Placement
{% highlight php %}
//Place in apache/htdocs/phpinfo.php
<?php
 phpinfo();
?>
{% endhighlight %}

PHPmyAdmin Re-route for PHPMyAdmin
{% highlight shell %}
//In c:\php\php.ini
#Uncomment "On windows:"
extension_dir 

extension=php_gd2.dll
extension=php_mbstring
extension=php_exif
extension=php_mysqli
{% endhighlight %}

PHPmyAdmin Re-route for PHPMyAdmin
{% highlight php %}
//Place in C:\apache\htdocs\phpmyadmin\config.inc
<?php
  $i=0;
  $i++;
  $cfg['Servers'][$i]['user']          = 'root';
  $cfg['Servers'][$i]['password']      = 'password';
  $cfg['Servers'][$i]['auth_type']     = 'config';
  $cfg['AllowUserDropDatabase']        = 'true';
?>
{% endhighlight %}

Permissions change

* wamp/alias/myalias.conf
* Allow from all
* Require local

Main htdocs Folders
{% highlight shell %}
C:\wamp\apache2\htdocs
C:\wamp\apps\phpmyadmin\htdocs
{% endhighlight %}

# Bitnami-Specific

index.php location (Using Bitnami)

* C:\wamp\apps\phpmyadmin\htdocs

Bitnami Manager/GUI

* C:\Bitnami\manager-windows

Bitnami Services(services.msc)  

  * wampstackApache
  * wampstackMySQL

# Troubleshooting
Finding port conflicts
{% highlight shell %}
netstat -a -o | find "LISTENING" | find ":80"
{% endhighlight %}

Skype Port 80
{% highlight shell %}
Skype -> Tools -> Advanced -> Connection -> Uncheck "Use port 80 and 443 for additional incoming connections."
{% endhighlight %}

Set/Reset mySQL password
{% highlight shell %}
mysql -u root -p
mysqladmin -u root -p password password
{% endhighlight %}

Config Port Manually
{% highlight shell %}
httpd.conf
Port->
"Listen 80"
"ServerName localhost:"
{% endhighlight %}
