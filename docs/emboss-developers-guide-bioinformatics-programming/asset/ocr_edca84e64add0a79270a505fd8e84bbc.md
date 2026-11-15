# ## 1.2.1 Downloading via CVS

To download via CVS you must have cvs installed on your system. It is there if an application is listed after typing:

```
which cvs
```

You must also use the secure shell SSH for the file transfer. Depending on your shell, type one of the following:

```
setenv CVS_RSH ssh
declare -x CVS_RSH=ssh
export CVS_RSH=ssh
```

To checkout the EMBOSS source code tree, go to the directory where you want the top-level EMBOSS directory created. For example to create EMBOSS in /home/auser/src/ you'd type:

```
cd /home/auser/src
```

To checkout EMBOSS you must first log on to the open-bio.org CVS server by typing:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss login
```

You will be prompted for a password which is cvs. You are now logged on to the CVS server. Checkout (download) EMBOSS by typing:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss checkout
emboss
```

This will take some time as it's downloading several megabytes of source code and data from the USA. Once the download is complete, terminate your CVS session with:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss logout
```

Here is a typical CVS session:

```
% declare -x CVS_RSH=ssh
% cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss login
Logging in to :pserver:cvs@cvs.open-bio.org:2401/home/repository/emboss
```