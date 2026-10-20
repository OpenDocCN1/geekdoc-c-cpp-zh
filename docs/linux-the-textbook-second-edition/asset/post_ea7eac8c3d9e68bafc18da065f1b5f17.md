
# Exercise 7.12

Give a command for displaying the lines in the ~/Personal/Phones file that contain phone numbers with area code 212. Phone numbers are stored as xxx-xxx-xxxx, where x is a digit from 0 to 9.

# Exercise 7.13

Display the names of all the files in your home directory that contain the word “main” (without quotes). What command did you use?

# Exercise 7.14

Display the names of all the files in your home directory that contain the word “main” (without quotes). What command did you use?

## 7.6 Cutting and Pasting

You can process files that store data in the form of tables in Linux by using the cut and paste commands. A table consists of lines, each line comprises a record, and each record has a fixed number of fields. Tabs or spaces usually separate fields, although any field separator can be used. The cut command allows you to cut one or more fields of a table in one or more files and send them to standard output. In other words, you can use the cut command to slice a table vertically in a file across field boundaries. The following is a brief description of the command.

```
Syntax:
cut -blist [-n] [file-list]
cut -clist [file-list]
cut -flist [-dchar] [-s] [file-list]
Purpose: Cut out fields of a table in a file
Output: Fields cut by the command
Commonly used options/features:
-b list    Treat each byte as a column and cut bytes specified in the list
-c list    Treat each character as a column and cut characters specified in the list
-d char    Use the character char instead of the <Tab> character as field separator
-f list    Cut fields specified in the list
-n         Do not split characters (used with -b option)
-s         Do not output lines that do not have the delimiter character
```

Here, list is a comma-separated list, with - used to specify a range of bytes, characters, or fields. The following sessions illustrate some of the commonly used options and features of the cut command. In this section, we use the file student_addresses, whose contents are displayed by the cat command.

```
$ cat student_addresses
John    Doe      jdoe@xyz.com    312.111.9999    312.999.1111
Pam     Meyer    meyer@uop.pk    666.222.1212    666.555.1212
Jim     Davis    jamesd@aol.org  713.999.5555    713.413.0000
Jason   Kim      j_kim@up.org    434.000.8888    434.555.2211
Amy     Nash     nash@state.gov  888.111.4444    888.827.3333
$
```

The file has five fields numbered 1–5, from left to right: first name, last name, e-mail address, home phone number, and work phone number. Although we could have used any character as the field separator, we chose the <Tab> character to give a “columnar” look to the table and the output of the following cut and paste commands. You can display a table of first and last names by using the -f option. Note that -f1,2 specifies the first and the second fields of the student_addresses file.

```
$ cut -f1,2 student_addresses
John  Doe
Pam   Meyer
Jim   Davis
Jason Kim
Amy   Nash
$
```

We generate a table of names (first and last) and work phone numbers by slicing the first, second, and fifth fields of the table in the student_addresses file.

```
$ cut -f1,2,5 student_addresses
John  Doe   312.999.1111
Pam   Meyer 666.555.1212
Jim   Davis 713.413.0000
Jason Kim   434.555.2211
Amy   Nash  888.827.3333
$
```

To generate a table of names and e-mail addresses, we use the following command. Here, -f1-3 specifies fields 1–3 of the student_addresses file.

```
$ cut -f1-3 student_addresses
John  Doe   jdoe@xyz.com
Pam   Meyer meyer@uop.pk
Jim   Davis jamesd@aol.org
Jason Kim   j_kim@up.org
Amy   Nash  nash@state.gov
$
```

We recommend that you run this command on your machine to determine whether the desired output is produced. If the desired output is not produced, you have not used the <Tab> character as the field separator for some or all of the records. In such a case, correct the table and try the command again.

In the preceding sessions, we have used the default field separator, the <Tab> character. Depending on the format of your file, you can use any character as a field separator. For example, as we discussed in Chapter 4, the /etc/passwd file uses the colon character (:) as the field separator. You can therefore use the cut command to extract information, such as the login name, real name, group ID, and home directory for a user. Because the real name, login name, and home directory are the fifth, first, and sixth fields, respectively, the following command can be used to generate a table of names of all users, along with their login IDs and home directories. The first two lines of the output are for comments, as they start with #.

```
$ cut -d: -f5,1,6 /etc/passwd
# $FreeBSD$
#
root:Charlie &:/root
toor:Bourne-again Superuser:/root
daemon:Owner of many system processes:/root
...
sshd:Secure Shell Daemon:/var/empty
smmsp:Sendmail Submission User:/var/spool/clientmqueue
...
sarwar:Syed Mansoor Sarwar:/home/sarwar
...
$
```

Note that the -d option is used to specify : as the field separator, and it is also displayed as the field separator in the output of the command. For blank delimited files, use one or more space characters (blanks) after -d\, as shown in the following example. The cat sample command is used to display the blank delimited file, called **sample**, and the cut -d\  -f1,6 sample command is used to display fields 1 and 6 of this file.

```
$ cat sample
1 John CS Senior john@net2net.com 3.45
2 Jane CS Junior jane@net2net.com 3.76
3 Sara CS Senior sara@net3net.vom 3.33
$ cut -d\  -f1,6 sample
1 3.45
2 3.76
3 3.33
$
```

The **paste** command complements the cut command; it concatenates files horizontally (the cat command concatenates files vertically). Hence, this command can be used to paste tables in columns. The following is a brief description of the command.

**Syntax:**
**paste [options] file-list**
**Purpose:** Horizontally concatenate files in **file-list**; use standard input if - (i.e., a hyphen) is used as a file
**Output:** Files in **file-list** pasted (horizontally concatenated)
**Commonly used options/features:**
**-d list**    Use list characters as line separators; **<Tab>** is the default character

Consider the file **student_records**, which contains student names (first and last), major, and current Grade Point Average (GPA).

```
$ cat student_records
John  Doe    ECE   3.54
Pam   Meyer  CS    3.61
Jim   Davis  CS    2.71
Jason Kim    ECE   3.97
Amy   Nash   ECE   2.38
$
```

We can combine the two tables, **student_records** and **student_addresses_shortened**, horizontally and generate another by using the paste command in the following session. To keep the resultant table small, we have used a shortened version of the original **student_addresses** file called **student_addresses_shortened**, which contains the first name, last name, and work phone number only. We generated this table by using the cut -f1,2,5 student_addresses > student_addresses_shortened command. Note that the output of the paste command is displayed on the display screen and is not stored in a file. The resultant table has seven fields.

```
$ cat student_addresses_shortened
John  Doe   312.999.1111
Pam   Meyer 666.555.1212
Jim   Davis 713.413.0000
Jason Kim   434.555.2211
Amy   Nash  888.827.3333
```

```
$ paste student_records student_addresses_shortened
John  Doe   ECE   3.54  John  Doe   312.999.1111
Pam   Meyer CS    3.61  Pam   Meyer 666.555.1212
Jim   Davis CS    2.71  Jim   Davis 713.413.0000
Jason Kim   ECE   3.97  Jason Kim   434.555.2211
Amy   Nash  ECE   2.38  Amy   Nash  888.827.3333
$
```

Suppose that you want to use the student_addresses_shortened and student_records tables to generate and display a table that has student names, majors, and home phone numbers. You may do so in one of two ways. When you use the first method, you cut the appropriate fields of the two tables, put them in separate files with the fields in the order you want to display them, paste the two tables in the correct order, and remove the tables. The following session illustrates this procedure and its result. Note that the new table is not saved as a file when the following commands are executed. If you want to save the new table in a file, use the paste table1 table2 > students_table command. The students_table contains the columns of table1 and table2 (in that order) pasted together.

```
$ cut -f1-3 student_records > table1
$ cut -f4 student_addresses > table2
$ paste table1 table2
John Doe ECE 312.111.9999
Pam Meyer CS 666.222.1212
Jim Davis CS 713.999.5555
Jason Kim ECE 434.000.8888
Amy Nash ECE 888.111.4444
$ rm table1 table2
$
```

The procedure just outlined is expensive in terms of space and time because you have to execute four commands, generate two temporary files (table1 and table2) on disk, and remove these temporary files after the desired table has been displayed. You can use a different method to accomplish the same thing with the following command.

```
$ paste student_records student_addresses | cut -f1-3,8
John Doe ECE 312.111.9999
Pam Meyer CS 666.222.1212
Jim Davis CS 713.999.5555
Jason Kim ECE 434.000.8888
Amy Nash ECE 888.111.4444
$
```

Here, you first combine the tables in the two files into one table with nine columns by using the paste student_records student_addresses command and then displaying the desired table by using the cut -f1-3,8 command. Clearly, this second method is the preferred way to accomplish the task because no temporary files are created and only one command is needed. If you want to save the resultant table in the students_table file, use the command paste student_records student_addresses | cut -f1-3,8 > students_table.

# Exercise 7.15

Create the student_addresses and student_records files used in Section 7.6. Then, run the cut and paste commands described in this section to see how these commands work.

## 7.7 Compressing Files

Reduction in the size of a file is known as file compression, which has both space and time advantages. A compressed file takes less disk space to store, less time to transmit from one computer to another in a network or Internet environment, and less time to copy. It takes time to compress a file, but if a file is to be copied or transmitted several times, the time spent compressing the file could be just a fraction of the total time saved. In addition, if the compressed file is to be stored on a secondary storage device (e.g., a disk) for a long time, the savings in disk space can be considerable. Another consequence of compression is that a compressed file reads as garbage. However, this is not a problem because the process is fully reversible and a compressed file can be converted back to its original form. If you can fully recover the original file from its compressed version, the compression is known as lossless compression.
