# Setting up your System

This book presumes you are using the Linux operating system with either the KDE3.5, KDE4, or Gnome desktop. Specific instructions are included for Ubuntu (and Kubuntu) and OpenSuse 11.

If you are using the KDE desktop you will have Konqueror or Dolphin as the File Manager and kate or kedit for an editor

In Gnome you would probably use Nautilus and gedit

You need to be familiar with the idea of doing some things as “super user” so that you have access permission to copy or edit certain files. This is normally done by prefixing the Linux command with “sudo” and providing the password, as in this example:

```
`“sudo cp hello3 /srv/www/cgi-bin/hello3”`
```

which copies the file “hello3” to the area where the Apache server locates common gateway interface or cgi programs.

In KDE “kdesu konqueror” would open a file manager as super user.

In Gnome “gnomesu nautilus” would open a file manager as super user.

You will need to have installed the following packages:

| package | Ubuntu | Open Suse |
|---|---|---|
| C development libraries | build-essential | Base Development (pattern) |
| Apache web server | apache2 | Web and LAMP Server (pattern) |
| Apache development libraries | apache2-prefork-dev | apache2-devel |
| MySQL server, client and development libraries | mysql-server libmysqlclient15-dev | libmysqlclient-devel |
| GD and development libraries | libgd2-xpm | gd<br>gd-devel |

Throughout the text you will see references to the folder **cgi-bin**. The location of this will vary between Linux distributions. By default this folder used for web programs is:

+   - OpenSuse: **/srv/www/cgi-bin**

+   - Ubuntu: **/usr/lib/cgi-bin**