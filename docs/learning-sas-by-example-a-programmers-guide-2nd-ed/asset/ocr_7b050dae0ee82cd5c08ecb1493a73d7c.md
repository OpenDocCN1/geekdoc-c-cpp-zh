# 3.6 Reading Data Values Separated by Delimiters Other Than Blanks, Commas

Remember that the default delimiter for list input is a blank. Using the INFILE option DSD changes the default to a comma. What if you have a file with other delimiters, such as tabs or colons? No problem! You only need to add the DLM—option to the INFILE statement. For example, the following lines of data use colons as delimiters.

Example of a file using colon delimiters:

```
M:50:68:155
F:23:60:101
M:65:72:220
F:35:65:133
M:15:71:166
```

To read this file, you could use this INFILE statement:

```
infile 'file-description' dlm=';';
```

You can spell out the name of the DELIMITER=option instead of using the abbreviation DLM if you like, for example:

```
infile 'file-description' delimiter=';';
```

You can use the DSD and DLM—options together. This combination of options performs all the actions requested by the DSD option (see Section 3.4) and overrides the default DSD delimiter (comma) with a delimiter of your choice.

```
infile 'file-description' dsd dlm=';';
```

Tabs present a particularly interesting problem. What character do you place between the quotes on the DLM—option? You cannot click the TAB key. Instead, you need to represent the tab by its hexadecimal equivalent. For ASCII files (the coding method used on Windows platforms and UNIX operating systems—it stands for American Standard Code for Information Interchange), you would use the following:

```
infile 'file-description' dlm='09x';
```

For EBCDIC files (used on most mainframe computers—it stands for Extended Binary-Coded Decimal Interchange Code), you would use the following statement:

```
infile 'file-description' dlm='05x';
```

> Note: These two values are hexadecimal constants. If you know (or look up) the hexadecimal value of any character, you can represent it in a SAS statement by placing the hexadecimal value in single or double quotes and following the value immediately (no space) by an upper- or lowercase x.