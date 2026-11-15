Give the corresponding memory snapshot, and the value of the stream state flags, after each of the following sets of statements is executed:

+   8. int i(0), j(0);
+      double x, y;
+      char ch1, ch2;
+      cin >> x >> y >> ch1 >> ch2;

+   9. int i(0), j(0);
+      double x, y;
+      char ch1, ch2;
+      cin >> x >> i >> j >> ch1 >> ch2;

+   10. int i(0), j(0);
+       double x, y;
+       char ch1, ch2;
+       cin >> i >> j >> ch1 >> ch2;

+   11. int i(0), j(0);
+       double x, y;
+       char ch1, ch2;
+       cin >> i >> j >> x >> ch1 >> ch2;

# Data Filters.

Programs called data filters are often used to read the information in a data file and then analyze the contents. In many cases, this data filter program is designed to remove any data errors that would cause problems with other programs that read the information from the data file. The next set of programs is designed to perform error checking and data analysis on information in a data file. Generate data files to test all features of the programs.

+   12. Write a program that reads a data file that should contain only integer values and thus should contain only digits, plus or minus signs, and whitespace. The program should print any invalid characters located in the file, and at the end it should print a count of the invalid characters located.

+   13. Write a program that analyzes a data file that has been determined to contain only integer values and whitespace. The program should print the number of lines in the file and the number of integer values (not integer digits).

+   14. Write a program that reads a file that contains only integers, but some of the integers have embedded commas, as in 145,020. The program should copy the information to a new file, removing any commas from the information. Do not change the number of values per line in the file.

+   15. Write a program that reads a file containing integer and floating-point values separated by commas, which may or may not be followed by additional whitespace. Generate a new file that contains the integers and floating-point values separated only by spaces; remove all whitespace characters between the values, and insert a single space between the values. Do not change the number of values per line in the file.

+   16. Write a program that reads a file containing data values computed by an accounting software package. While the file contains only numerical information, the values may contain embedded commas and dollar signs, as in $3,200, and negative values are enclosed in parentheses, as in (200.56). Write a program to generate a new file that contains the values with the commas and dollar signs removed, and with a leading minus sign instead of the parentheses. Do not change the number of values per line in the file.