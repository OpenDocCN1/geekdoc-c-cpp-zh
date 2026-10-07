# Learning SAS by Example: A Programmer’s Guide, Second Edition

SAS creates a temporary SAS data set called Test. When you close your SAS session, this data disappears. SAS data set names have two-part names in the format:

```
libref.data-set-name
```

The part of the name before the period is called a libref (short for library reference), and this tells SAS where to store (or retrieve) the data set. The part of the name after the period identifies the name you want to get the data set.

Until now, all the programming examples in this book used a data set without a period. When you use a name like Test in the DATA statement, SAS uses a default libref called Work that SAS creates every time you open a SAS session. For example, if you write a DATA statement such as

```
data Test;
```

SAS adds the default libref Work, so this DATA statement is equivalent to

```
data Work.Test;
```

All that is required to make your SAS data sets permanent is to create your own libref using a LIBNAME statement and use libref in the two-level SAS data set name.

Suppose you want to create a permanent SAS data set called Test_Scores in your C:\learning folder. You can do this using the following:

# Program 4.1: Creating a Permanent SAS Data Set

```
libref Mozart 'C:\learning\';
ndata Mozart.Test_Scores;
  length ID $ 3 Name $ 15;
  input ID $ Score-Score3 Name $;
datalines
  1 90 95 98 Jan
  2 78 77 99 Preston
  3 88 91 92 Russell
;
```

The LIBNAME statement starts with the keyword LIBNAME and then specifies the name of the library (called a libref), followed by the directory or folder where you want to store your permanent SAS data sets. The libref must not be more than 8 characters and must be a valid SAS name.

When you run this program, data set Test_Scores becomes a permanent data set in C:\learning. Any libref you create exists only for your current SAS session. If you open a new SAS session, you need to reissue that LIBNAME statement. A good way to think of a libref is an alias for the folder (on Windows or UNIX platforms). On mainframe computers, a SAS library is actually a single file that can hold multiple data sets.

If you run Program 4.1 on a Windows platform, the data set will be stored as the data set called Test_Scores, and it will be stored in the file Test_Scores.sas7dat in the C:\learning folder. The file extension stands for SAS binary data version 7. You might wonder why there is a 7 rather than a 9 in the file extension when created using SAS9. Since the structure of SAS data sets has not changed since SAS 7, SAS has maintained the same file extension used in SAS 7.