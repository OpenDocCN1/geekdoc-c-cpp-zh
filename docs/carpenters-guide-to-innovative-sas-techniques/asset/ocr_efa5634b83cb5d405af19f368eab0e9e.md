When working with EXCEL typical LIBNAME options might include:

+   - HEADER: Determines if a header row exists or should be added to the table.
+   - MIXED: Some columns contain both numeric and character information.
+   - VER: Controls which type (version) of EXCEL is to be written.

# ### Data Source Options

Some of the same options associated with PROC IMPORT (see Section 1.2.3) can also be used on the LIBNAME statement. These include:

+   - GETNAMES: Incoming variable names are available in the *first row* of the incoming data.
+   - SCANTEXT: A length is assigned to a character variable by scanning the incoming column and determining the maximum length.

# ### 1.1.4 Replacing EXCEL Sheets

While the EXCEL engine allows you to establish, view, and use a sheet in an Excel workbook as a SAS data set, you cannot update, delete or replace the sheet from within SAS. It is possible to replace the contents of a sheet, however, with the help of PROC DATASETS and the SCAN_TEXT=NO option on the LIBNAME statement. The following example shows how to replace the contents of an EXCEL sheet.

In the first DATA step the programmer has 'accidently' used a WHERE clause ❶ that writes the incorrect data, in this case 0 observations, to the EXCEL sheet. Simply correcting and rerunning the DATA step ❷ will not work because the sheet already exists.

```
```sas
libname tocls excel "&path\data\newb.xls";

data tocls.ClinicNames;
set advrpt.clinicnames;
where clinnames>'X';❶
run;

* Running the DATA step a second time
* results in an error;
data tocls.ClinicNames;❷
set advrpt.clinicnames;
run;
```
```

We could step out of SAS and use EXCEL to manually remove the bad sheet, however, we would rather do it from within SAS. First we must reestablish the libref using the SCAN_TEXT=NO option ❸. PROC DATASETS can then be used to delete the sheet. In actuality the sheet has not truly been deleted, but merely cleared of all contents. Since the sheet is now truly empty and the SCAN_TEXT option is set to NO, we can now replace the empty sheet with the desired contents.

```
```sas
libname tocls excel
"&path\data\newb.xls"
scan_text=no ❸;
proc datasets library=tocls nolist;
delete ClinicNames;
quit;
```
```

has not truly been deleted, but merely cleared of all contents. Since the sheet is now truly empty and the SCAN_TEXT option is set to NO, we can now replace the empty sheet with the desired contents.