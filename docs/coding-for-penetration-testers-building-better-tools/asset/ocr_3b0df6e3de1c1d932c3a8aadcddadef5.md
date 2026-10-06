Autonomous LAN Party is an application to help run LAN parties. Due to a RFI vulnerability, it is also an application to allow Web server access. You can find out more about the vulnerability on exploit-db.com at http://www.exploit-db.com/exploits/9460/. Once we download the source from the location indicated in the vulnerability reference, we can unzip and copy it to our Web root at /var/www/html/alp.

Now that we have the code in place, we could install it. But to demonstrate this vulnerability, we don't have to. Let's look at the code for the vulnerable page at /var/www/alp/include/_bot.php:

```
<?php require_once $master['currentskin']._bot.php; ?>
<body></html>
```

This is an example of a file that is intended to be included in another script. But, in this instance, it can be called on its own. The file is using require_once to include the current skin's copy of _bot.php. The problem is that without the configuration information, the script doesn't know what $master['currentskin'] is. Maybe we can help. By default, though, our server is configured to be fairly secure. Let's fix so that we can emulate a server we might come across in the wild.

We need to change one variable in the /etc/php5/apache2/php.ini file and add a line of code. We have to add the line of code after PHP 5.4, they disabled a feature called register_globals. We will discuss that feature as we work on our exploit. However, we will still need to modify our favorite php.ini for apache2 to enable url includes. To do this we use our favorite editor and open the file and search for register_globals. We change it from Off to On. Next, we will search for allow_url_include and change it from Off to On. Now we will save the file and use the command apache2 restart. vulnerable Web service.

Next we may modify the /var/www/alp/include/_bot.php so that it the emulation for register_globals in the code will look like:

```
<?php
extract($_REQUEST); require_once
```