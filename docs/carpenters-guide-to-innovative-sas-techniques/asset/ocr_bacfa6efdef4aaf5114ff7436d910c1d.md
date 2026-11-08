# 15.1  A Few Miscellaneous Tips

Here are just a few of many tips.

# SEE ALSO

If you want more tips read the ‘Tip of the Day’ on sasCommunity.org. You can even have the tip tweeted to you.

# 15.1.1  Customizing Your NOTEs, WARNINGs, and ERRORs

The PUT, PUTLOG, and %PUT statements can be used to generate customized notes, warnings, and errors in the LOG. Since these statements are executable, logic can be used to conditionally execute them. The text written to the LOG follows the systems conventions when the statement keyword is immediately followed by one of the following:

+   - NOTE:        The note is written in blue.
+   - WARNING:     Warnings are written in green.
+   - ERROR:       Errors are written in red and are summarized along with other errors.

The keyword must be capitalized and must be immediately followed by a colon.

```
```sas
lock sashelp.class;
%put NOTE: class should be locked;
```
```

```
```text
41    lock sashelp.class;
NOTE: SASHELP.CLASS data is now locked for exclusive access by you.
42    %put NOTE: class should be locked;
NOTE: class should be locked
```
```

You can also follow the words NOTE, WARNING, or ERROR with a dash instead of a colon. The customized message will still appear in the LOG with the appropriate color; however, the word NOTE, WARNING, or ERROR will not appear.

# SEE ALSO

Don Henderson wrote a tip on sasCommunity.org that discusses this topic
http://www.sascommunity.org/wiki/Tips:Using_NOTE,_WARNING,_ERROR_in_Your_Program%27s_Generated_Messages.