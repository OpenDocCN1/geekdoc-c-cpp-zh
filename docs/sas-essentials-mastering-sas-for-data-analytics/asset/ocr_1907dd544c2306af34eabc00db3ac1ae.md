# SPECIFYING THE ODS OUTPUT FORMAT AND DESTINATION 195

The file names following the ODS output format are optional, SAS may prompt you for a file name if it is omitted. Note that when you specify a file name in Windows, it must include the correct extension for Windows to recognize the output file type. For example, to send data to a PDF file, you could use the following syntax:

```
ODS PDF file='WINDOWS-PATH\Filename.PDF';
```

or, as a specific example:

```
ODS PDF FILE='C:\SASADATA\MYOUTPUT.PDF';
```

If you leave off the destination, as in

+   ODS PDF;
... some procedures
ODS CLOSE PDF;

SAS will send the output to the SAS Results Viewer window without prompting you for a file name. For output formats such as PDF and RTF, if you do not indicate a file name, you may be prompted to enter one (or you may choose to have the results go into the SAS Results Viewer). When you use the default HTML output format, you are not prompted for a name.

It is important to remember that if you specify an ODS output, you also need to close it to SAS finishing the output to that location. If you do not close the location, you may not be able to see the results. For example, if you use ODS RTF; to open the RTF (Word) output, you then must at some point close with the statement ODS RTF CLOSE;. Thus, the statements would be

```
ODS RTF;
SAS code that produces output...
ODS RTF CLOSE;
```

Beginning with SAS 9.2 the default output location became HTML (Previously it was LISTING.) Beginning with SAS Version 9.4, the output defaults are as follows:

+   - Default output is HTML and the default style is HTMLBlue
- ODS Graphics is on
- Listing is closed

However, if you use the ODS statement to close the HTML location (ODS HTML CLOSE;), SAS may not produce any output. This will cause an error message in the log that indicates there is no output destination open. If this happens, you should reset the HTML default option in SAS. Use this statement:

```
ODS PREFERENCES;
```

to restore the default HTML output settings.