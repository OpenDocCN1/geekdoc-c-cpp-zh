The configuration of the server can be a bit fiddly but in OpenSuse we have to add this to the file

**/etc/apache2/default-server.conf**

```
<Location /labelmaker>
    SetHandler labelmaker
</Location>
```

and in **/etc/config.sys/apache2** we **add** the name of our module labelmaker to long comma-separated list in the line starting

```
APACHE_MODULES=".....labelmaker"
```

Now go to the folder labelmaker and type:

```
sudo /usr/sbin/apxs2 -c -i mod_labelmaker.c
sudo /etc/init.d/apache2 restart
```

Please click the advert

![](bbox=[0.12, 0.62, 0.93, 0.9])