mingw32-make to correctly build usingcmd.exe.

+   2. Manually copy theplugins.pdp.winfile to the bin directory, rename itplugins.pdp, delete line 16 (line beginning win32:QMAKE_PRE_LINK+=) fromhyperbolicLnPlugin.pro, rerun qmake, and then rerunmingw32-make.

+   3. Modify line 16 ofhyperbolicLnPlugin.pro to use the Unixcp instead of the Windowscopy command. To do this, simply replace the line with

```
win32:QMAKE_PRE_LINK+=cp $$PWD
../../plugins.pdp.win
$$HOME/bin/plugins.pdp
rerunqmake, and rerunmingw32-make.
```

Finally, I do understand that it can be extremely frustrating to invest time (and possibly money) on a new book and find that you cannot build the accompanying source code per the author’s instructions. If you’ve tried unsuccessfully to fix a build or runtime