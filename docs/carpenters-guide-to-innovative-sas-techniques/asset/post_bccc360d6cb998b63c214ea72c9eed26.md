
❻ The tailored configuration file is pointed to using a second -CONFIG initialization option on the execution line:

```text
-config "C:\\InnovativeTechniques\\SASCode\\Chapter14\\E14_3_1.cfg"
```

This option will generally be in addition to the standard configuration file which will also use a -CONFIG option.

```sas
proc options option=sasautos;
   run;
%put %sysget(advtech);
```

❼ We can confirm the values in the SASAUTOS option by using PROC OPTIONS.

❽ The value of the ADVTECH environmental variable can be surfaced using the %SYSGET macro function.

The LOG shows that the SASAUTOS option has been modified and that the ADVTECH environmental variable has the anticipated value. Notice that the SASAUTOS fileref is not quoted ❼ in the LOG. If we had inserted the additional locations without first inserting the parentheses, this text would have been quoted and that portion of the autocall library would not have been available.

```text
5    proc options option=sasautos;
6       run;

     SAS (r) Proprietary Software Release 9.2  TS2M2

SASAUTOS=('!advtech\\SASMacros\\' '!advtech\\ProdMacros\\' sasautos ) ❼
                         Search list for autocall macros
NOTE: PROCEDURE OPTIONS used (Total process time):
      real time           0.00 seconds
      cpu time            0.00 seconds
7
8    %put %sysget(advtech);
C:\\InnovativeTechniques\\SASCode ❽
```

Other common initialization options that could be declared in this second configuration file could include:

- `-SASINITIALFOLDER` (see Section 14.1.1)
- `-AUTOEXEC` (see Sections 14.1.1 and 14.2)
- `-VERBOSE` Show option setting in the log at initialization

### SEE ALSO

SAS Problem Note 44791 discusses the problem associated with inserting an autocall location, but does not suggest the solution worked out by Peter Crawford http://support.sas.com/kb/44/791.html. Sample Code 42360 demonstrates the use of the APPEND option http://support.sas.com/kb/42/360.html.

## 14.3.2 Controlling DM Initialization

When the Display Manager is initialized you can, to a large extent, control the appearance and the available tools through the use of initialization options. This level of control is most generally of interest when you are executing an application, perhaps through SAS/AF or SAS/EIS, and you need to control your user’s ability to access SAS.

![](img/4b16455363806a3241267bf9f49ba5d1_477_0.png)

- The entire top line can be turned off by using:

```text
-AWSCONTROL NOTITLE
```

Alternatively you can change the title from the default (SAS) to one of your choosing:

```text
-AWSTITLE "ABC Project"
```

- The list of drop-down menus can be turned off by using the -NOAWSMENU initialization option.

```sas
/* Prep for AF start up application */
-initcmd   af=ccontrol.Control.wrapper.frame af;
           toolclose;
           zoom;
           command close;
           wstatus off;
           wwindow off;"
```

The -INITCMD option allows you to specify control commands when executing an application, such as SAS/AF. The initialization option shown here starts a SAS/AF application and closes most of the user’s access to the rest of SAS.

## 14.4 In the Display Manager

The Display Manager is extremely customizable. Many of these possible customizations are a bit over the top, but there are a number that are very helpful.

### SEE ALSO

Richard DeVenezia's Web site has a useful section on "actions" you might consider adding to the explorer window http://www.devenezia.com/downloads/sas/actions/

## 14.4.1 Showing Column Names in ViewTable

By default the VIEWTABLE window displays variable labels as column headers. I find this to be very annoying as I almost always want to see the variable name. Fortunately the default can be changed to show the column names instead of the labels.

![](img/4b16455363806a3241267bf9f49ba5d1_478_0.png)

Although the following steps will be basically the same, the setup of some of the following dialog boxes will vary according to OS and version of SAS.

![](img/4b16455363806a3241267bf9f49ba5d1_478_1.png)

With the SAS Explorer Window active, select: TOOLS → OPTIONS → EXPLORER

This brings up the Explorer Options dialog box, select: MEMBERS → TABLE → EDIT

Edit the line with the ACTION of &OPEN and add colheading= name. The default for VIEWTABLE will now be to display variable names. Repeat the process for VIEWS.

![](img/4b16455363806a3241267bf9f49ba5d1_478_2.png)

### MORE INFORMATION

Rather than change the default behavior you can also change this setting when the ViewTable is invoked. Section 14.4.2 shows a DM command that invokes the ViewTable using column names rather than labels.

## 14.4.2 Using the DM Statement

The DM statement allows you to execute one or more Display Manager commands from within a SAS program. These are some commands that can be used in the command box, on the command line, or from the KEYS window.

```sas
DM <windowname> 'action' <windowname>;
```

If you do not need to designate or change the active window all you need is the action. This is common when performing a DM task from within a batch program.

The following command can be used to clear the LOG window.

```sas
dm log 'clear';
```

Multiple DM commands can be included in a single DM statement by chaining them together with semicolons. This DM statement turns off the program editor and executes a SAS/AF program making the SAS/AF window active.

```sas
dm af "pgm off; af cat = appls.allproj.passwd.program";
```

You can also route the LOG much as you can by using PROC PRINTTO.

```sas
dm 'log; file "&path\\logdump1.log"';
```

The POST command can be used to post a message box to the users screen. This can be a much stronger attention grabber than just a message to the LOG.

```sas
dm 'post "this is a message"';
```

![](img/4b16455363806a3241267bf9f49ba5d1_479_0.png)

The enhanced editor is designated using the WEDIT command, and if followed by a filename, a specific file can be loaded and opened for editing.

```sas
dm 'wedit "C:\InnovativeTechniques\sascode\chapter14\e14_3_1.sas"';
```

The ViewTable can be invoked as well using either the VIEWTABLE or VT command. Here the data set ADVPRT.DEMOG is opened with the variable names shown as column headings (COLHEADING=LABELS is the default).

```sas
dm "viewtable advprt.demog colheading=names";
```

The DM statement can also be used to assign a specific command to a function key (see Section 14.4.7). The KEYDEF command is used to make the assignment. Here the F12 key is assigned to clear the log.

```sas
dm 'keydef f12 "log;clear"';
```

For combination keystrokes enclose the key definition in quotes as well. The SHIFT F9 key will now close the next open ViewTable window. Close a series of open ViewTable windows with successive selections.

```sas
dm 'keydef "shf f9" "next VIEWTABLE;"; end';
```

### MORE INFORMATION

The DM statement is used to execute the DMOPTSAVE and DMOPLOAD commands in Section 14.1.3. Section 14.4.7 discusses the execution of DM commands through hot key assignments.

### SEE ALSO

The DM statement and the WEDIT command are discussed in the SAS Forum thread http://communities.sas.com/thread/12520. Rosenbloom and Lafler (2011c) assign a macro call to a function key.

## 14.4.3 Enhanced Editor Options and Shortcuts

There are a number of options and shortcuts available for use with the Enhanced Editor. It is also possible to do a fair amount of customization.

### Enhanced Editor Setup

There are only a few set up preferences that I would recommend that you change. Most of the defaults are fine for typical users. The options for the Enhanced Editor can be found when the editor is the active window. Use TOOLS → Options → Enhanced Editor. This brings up the Enhanced Editor Options dialog box.

![](img/4b16455363806a3241267bf9f49ba5d1_480_0.png)

I like to select ‘Show Line numbers’ because it makes life easier for large programs. More importantly, be sure to check ‘insert spaces for tabs’ and ‘replace tabs with spaces on file open’. Both of these options help to make it easier to maintain the text

![](img/4b16455363806a3241267bf9f49ba5d1_480_1.png)

formatting of a SAS program when it is transferred between programmers.
