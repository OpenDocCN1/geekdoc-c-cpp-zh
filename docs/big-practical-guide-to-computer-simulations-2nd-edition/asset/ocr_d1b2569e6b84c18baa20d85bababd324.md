```
[general]
auth-access = write
password-db = passwd
realm = This repository contains ...
```

The first line contains a tag, the second states that only authenticated users have write access to the repository, i.e. only they can commit files. The third line states the password file as entered above. The fourth line should describe your repository. Here, you should put a meaningful short description, which will be shown when logging in. When using senserve, you should use URLs starting with svn:// for the commands instead of URLs beginning with file:// as above, for example for the commands checkout or list:

```
svn checkout svn://svn.physik.uni-oldenburg.de/hartmann/repos1
```

All commands, where no URL is passed as argument, such as update and commit, work like in the single-user case.

Another access method to subversion repositories is based on the Apache server, in this case the URLs will begin with the standard http:// prefix. Details about the server configuration with Apache, also more information for the senserve case, can be found in the documentation [SVN].