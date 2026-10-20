+   - Airline reservation systems that display arrival and departure times for flights sorted according to flight numbers at airport terminals
+   - Names of people displayed in a pharmacy with ready prescriptions
+   - Names of students listed in class lists coming from the registrar’s office

The sorting process is based on using a field, or portion of each item, known as the sort key. To determine the position of each item in the sorted list, you compare the items in a list (usually two at a time) by using their key fields. The choice of the field used as the key depends on the items to be sorted. If the items are personal records (e.g., student employee records), last name, student ID, and social security number are some of the commonly used keys. If the items are arrival and departure times for the flights at an airport, flight number and city name are commonly used keys.

The Linux sort utility can be used to sort items in text (ASCII) files. The following is a brief description of this utility.

**Syntax:**
`sort [options] [file-list]`
**Purpose:** Sort lines in the ASCII files in **file-list**
**Output:** Sorted files to standard output
**Commonly used options/features:**
`-b` Ignore leading blanks
`-d` Sort according to usual alphabetical order: ignore all characters except letters, digits, and then blanks
`-c` Check for sorted input; do not sort
`-f` Consider lowercase and uppercase letters to be equivalent
`-m` Merge already sorted files
`-n` Compare according to string numerical value
`+n1[-n2]` Specify a field as the sort key, starting with +n1 and ending at -n2 (or end of line if -n2 is not specified); field numbers start with 0
`-o FILE` Send sorted output to FILE instead of standard output
`-r` Sort in reverse order

If no file is specified in **file-list**, sort takes input from standard input. The output of the sort command goes to standard output. By default, sort takes each line, starting with the first column, to be the key and performs case-insensitive sort in alphabetic order. In other words, it rearranges the lines of the file—that is, strings separated by the newline character (\n)—according to the contents of all the fields, going from left to right. Thus, in the output of the sort command, lines starting with digits (0–9) appear before lines starting with letters, lowercase letters appear before their uppercase counterparts as in a, A, b, B, c, etc., and 1,000 is treated smaller than 3 because 3 is greater than that of 1 (first letter in 1,000). The following session illustrates these points.

```
$ cat data
100
Hello
war
Zoo
20
apple
World
200
April
40
```