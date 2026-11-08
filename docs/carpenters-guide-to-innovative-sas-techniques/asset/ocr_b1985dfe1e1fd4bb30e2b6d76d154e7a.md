![](bbox=[0.21, 0.09, 0.42, 0.18])

![](bbox=[0.49, 0.09, 0.7, 0.18])

![](bbox=[0.74, 0.09, 0.92, 0.18])

When using the RTF style in the RTF destination, changing the background color (BC=) adds a box around the title.

In RTF, by default, the titles and footnotes are added to the HEADER and FOOTERS of the document when the table is imported. Footers are at the bottom of the physical page, and not necessarily at the bottom of the table. The titles/footnotes can be made a part of the table itself through the use of the BODYTITLE option. For shorter tables this can move the footnote to the base of the table.

```
```
ods rtf file="&path\results\E9_1b.rtf"
    style=rtf
    bodytitle;
```
```

Through the use of the background color option (BCOLOR) you can change the background color behind the title's text. This option can also be used to create colorful horizontal lines. ➊ The BCOLOR option specifies the background color. ➋ Some text, if only a blank space, must be specified.

```
```
title1 '9.1c Horizontal Lines';
title2 h=5pt bcolor=blue ' '; ➊
footnote h=5pt bcolor=blue ' '; ➋
ods html file="&path\results\E9_1c.html";
proc print data=sashelp.class(obs=4);
run;
ods html close;
```
```

![](bbox=[0.58, 0.47, 0.88, 0.65])

There are quite a few other SAS/GRAPH TITLE statement options. Most of these options are ignored outside of SAS/GRAPH. Depending on the destination and style, some SAS/GRAPH TITLE statement options are occasionally not ignored (when you think that they should be). In these cases they tend to yield unanticipated results.