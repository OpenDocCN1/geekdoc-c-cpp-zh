# 14.1.6 Comments

Just like code, it is helpful to occasionally put comments in your XML. A comment begins with '<!--' and ends with '-->'. You can put whatever text you want between them as long as it does not include the sequence to end the comment.

# 14.1.7 Overall Format

There are two other rules that are significant for XML. First, the entire XML document must be inside of a single element. In the example above, everything was the course element. If we wanted to have more than one course element, we would have had to create some higher level element to hold them.

In addition, most XML files will begin with an XML declaration that comes right before the element containing the XML document. The declaration has a slightly different syntax and might look like the following line.

```
<?xml version="1.0" encoding="UTF-8"?>
```

# 14.1.8 Comparison to Flat File

To better understand the benefit of XML, we will compare our XML file to a flat file that might be used to store basically the same information. Here is a flat file representation of the grade information from the XML above.

+   CSCI 1320
2
Quinn Bender
98 100 90
90
100
Jason Hughes
85 78
67
20

This is a lot shorter, unless you happen to know what it is encoding, you cannot figure much out it. Namely, the numbers in the file are hard to distinguish. The 2 near the top you might be able to figure out, but without additional information, it is impossible to determine which lines of grades are assignments, quizzes, or tests.

The flat file also lacks some of the information that was in the XML. In particular, the comments on the assignments in the XML format are missing in this file. It would be possible to make the flat file contain such information, but doing so would cause the code required to parse the flat file to be much more complex.

# 14.1.8.1 Flexibility in XML

A significant "Catch-22" of XML is that there are lots of different ways to express the same information. For example, the comment could have been given as an attribute with the name comment instead as contents of the element. Similarly, if you do not want to allow comments, you could shorten the XML to be more like the flat file by changing it to the following format.