
If loaded, the *Web Server Configuration Display* (`mod_info`) module will make all configuration files available, even down to the directory level (think `.htaccess`). The security threat to your site is that this module will “leak” information about configuration directives to other parts of Apache. This could include such things as system paths, usernames and passwords, databases installed, and more. Not running this module in a production environment such as an Internet-facing server is strongly recommended.

Comment out the following line if it is found in the configuration file:

```
LoadModule info_module modules/mod_info.so
```

Part of a dedicated hacker’s effort will be to *enumerate* your website. In essence, that means that the hacker will attempt to find and name everything to map out the network and server. If installed, the `speling_module` module will attempt to find a *document* (that is, a resource such as a file) by comparing each document name in the requested directory against the requested document name without regard to case, and allowing up to one misspelling.

This scenario is perfect for continuing to ping a site with requests and see what files show up. Disabling this module (if it’s installed) is recommended. Comment out the following line in your configuration file if found:

```
LoadModule speling_module modules/mod_speling.so
```

Using the capability of the directory translations module, an attacker could easily enumerate the web server’s users. Disable the following if it is found in your configuration file, unless it is absolutely needed:

```
LoadModule userdir_module modules/mod_userdir.so
```

If you are not using your Apache server as a *proxy server* (gateway) to other servers, then ensure that the following lines (if they exist) are commented out:

```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_balancer_module modules/mod_proxy_balancer.so
LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
LoadModule proxy_http_module modules/mod_proxy_http.so
LoadModule proxy_connect_module modules/mod_proxy_connect.so
```

If you do not know what the proxy server is for, you likely do not need it. Having it on is very dangerous if the server is not fully secured.

> **NOTE** For more information about directives in Apache configuration files, see http://httpd.apache.org/docs/2.2/mod/quickreference.html.

## Disabling or Setting Up Proper Services

Although each Apache configuration is very different, understanding what programs start at boot time is important. This knowledge can give you a very good picture of what programs you should enable or disable. You’ll likely have services similar to those shown in Figure 5-9, which shows the services that start up on this particular server.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_166_0.png)

Take the time to check your server with the following command:

```bash
# chkconfig --list | grep :on
```

Investigate the services and, if you determine that you do not need one or more of them, disable the service using the following command:

```bash
# chkconfig service off
```

Replace the word service in that command with the service name, as shown here:

```bash
# chkconfig pure-ftpd off
```

This command disables the FTP server from running at the next restart.

### WHAT IS THAT SERVICE?

Occasionally, you may see a service running that you are unsure of. This is not a cause for alarm, but you may want to investigate further. To learn what RPM package (installation package) the service came from, run the following command:

```bash
$ rpm -qf /etc/init.d/servicename
```

This reveals what package installed it. It could easily be a dependency for another service.

You can also get a brief description of what the RPM package does by typing in the following command:

```bash
$ rpm -qi rpmname
```

Note that this command may not work on all distributions of Linux.

The one service you should have turned on is ModSecurity. Let’s take a closer look at this very important module.

### ModSecurity

ModSecurity (available from www.modsecurity.org) is an open source Web Application Firewall (WAF). Its job is to protect the web application layer against a variety of attacks that target weaknesses in a CMS and other web applications. It does this with a variety of defenses, including monitoring of the HTTP (web) traffic, a flexible rules engine, and real-time analysis of your traffic.

ModSecurity (or mod_security) works as a reverse proxy, and provides a virtual patch against attacks. Using this or another type of WAF is highly recommended.

The installation of mod_security is quite simple using yum:

```bash
# yum install mod_security
```

The default configuration likely will work for you, but given its flexible rules engine, you have the option of deploying highly customized configurations on it. The deeper details are beyond the scope of this book. The following sources can provide more information:

- *ModSecurity Handbook* (London, Feisty Duck, Ltd., 2010), written by the principal developer of ModSecurity, Ivan Ristic. For more information, see www.feistyduck.com/books/modsecurity-handbook/index.html.
- Another reference is a fairly well-documented guide to the installation of ModSecurity on Ubuntu, located at: www.thebitsource.com/infrastructure-operations/web-application/securing-apache-web-servers-modsecurity.

which is a tool that forces PHP scripts (like your CMS) to be executed with the permissions of their owners.

suPHP is a great tool to use to ensure that you are running PHP in a very secure fashion. If you are using a managed virtual private server (VPS) or dedicated server at a hosting company, a quick telephone call to the support staff can help you establish if you are running it.

The next method is to try to set folder permissions to 777. If you're running suPHP, you'll get a 500 Internal Error when you browse.

### phpinfo

PHP has a great method for examining the entirety of the settings. Using the phpinfo function provides a useful tool to have in your toolkit.

The steps listed here to execute the phpinfo function are very easy to follow, and the end results are invaluable:

1. Create a text file in the root directory and name it `phpinfo.php`. In that file, insert the following:

    ```
    <?php phpinfo(); ?>
    ```

2. Save the file and ensure that the permissions are set for 644.

3. From your browser type the following:

    ```
    http://www.yourdomain.com/phpinfo.php
    ```

A lot of information about your server and its environmental settings appears. Near the top of the screen, you should see an entry that resembles Figure 5-10.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_170_0.png)

**Figure 5-10:** suPHP installed

If you see apache in place of the words CGI/FastCGI, then you likely do not have suPHP installed.

PHP has many settings that can be tricky to catch. Fortunately, a free and open source tool is available that will give you a good evaluation of your settings, as discussed in the following section.

### PhpSecInfo

The PhpSecInfo tool, from a group of international experts in PHP security, the PHP Security Consortium (PHPSC), is built to evaluate your server’s setup and ensure that you have all the PHP holes closed. You can get the tool by visiting

```
http://phpsec.org/projects/phpsecinfo/
```

When run on your server, this tool will test for a number of issues that could affect your security. Figure 5-11 shows an example of one such warning.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_171_0.png)

**Figure 5-11:** Warning produced by PhpSecInfo tool

This warning appears in red. The various warnings and errors are color-coded. This particular error is telling you that the `force_redirect` directive is disabled. Note the “More information” link on the lower right, which provides you with a detailed explanation of this warning.

At the bottom of the report is the Test Results Summary, as shown in Figure 5-12. It states that 18 tests were run and 10 notices, meaning they need attention. It produced 2 items marked as severe.

![](img/8bd670d4939cf71dbd0c6123d1b834ff_171_1.png)

**Figure 5-12:** Test Results Summary

You should run this tool regardless of how long your server has been in production. You might find that you have a number of holes. Be sure to run it after any upgrade, or after any incidents that occur.

### php.ini

When you’re using suPHP, you can find a file in the root of most websites called `php.ini`. This file allows you to issue commands to the PHP Interpreter. As was previously stated, you can use this file in place of the `/etc/php.ini` file. Check with your host to ensure the server is running suPHP.

Using WinSCP, locate the `/etc/php.ini` file. If this file does not exist in this directory, it can and may exist in your `public_html` website directory.
