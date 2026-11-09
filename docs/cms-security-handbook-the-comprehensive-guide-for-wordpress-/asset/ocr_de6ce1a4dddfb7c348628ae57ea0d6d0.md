This command disables the FTP server from running at the next restart.

# WHAT IS THAT SERVICE?

Occasionally, you may see a service running that you are unsure of. This is not a cause for alarm, but you may want to investigate further. To learn what RPM package (installation package) the service came from, run the following command:

```
```bash
$ rpm -qf /etc/init.d/servicename
```
```

This reveals what package installed it. It could easily be a dependency for another service.

You can also get a brief description of what the RPM package does by typing in the following command:

```
```bash
$ rpm -qi rpmname
```
```

Note that this command may not work on all distributions of Linux.

The one service you should have turned on is ModSecurity. Let’s take a closer look at this very important module.

# ModSecurity

ModSecurity (available from www.modsecurity.org) is an open source Web Application Firewall (WAF). Its job is to protect the web application layer against a variety of attacks that target weaknesses in a CMS and other web applications. It does this with a variety of defenses, including monitoring of the HTTP (web) traffic, a flexible rules engine, and real-time analysis of your traffic.

ModSecurity (or mod_security) works as a reverse proxy, and provides a virtual patch against attacks. Using this or another type of WAF is highly recommended.

The installation of mod_security is quite simple using yum:

```
```bash
# yum install mod_security
```
```

The default configuration likely will work for you, but given its flexible rules engine, you have the option of deploying highly customized configurations on it. The deeper details are beyond the scope of this book. The following sources can provide more information:

+   - *Mod Security Handbook* (London, Feisty Duck, Ltd., 2010), written by the principal developer of ModSecurity, Ivan Ristic. For more information, see www.feistyduck.com/books/modsecurity-handbook/index.html.
+   - Another reference is a fairly well-documented guide to the installation of ModSecurity on Ubuntu, located at: www.thebitsource.com/infrastructure-operations/web-application/securing-apache-web-servers-modsecurity.