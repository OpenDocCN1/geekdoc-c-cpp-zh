+   - **Date**—Date informats and formats enable PROC SQL and SAS to determine the month, day, and year values of a date. The month value handles values from 1 through 12. The day value handles values from 1 through 31 and applies additional validations to a maximum of 28, 29, or 30 depending on the month in question. The year value handles values from 1 through 9999. Dates go back to 1582 and ahead to 20,000. When you enter a year value of 0001 and specify a format and a Yearcutoff value of 1920, the returned value would be 2001.
+   - **Time** —Time informats and formats enable PROC SQL to determine the hour, minute, and second values of a time. The hour portion handles values from 00 through 23. The minute portion handles values from 00 through 59. The second portion handles values from 00 through 59.
+   - **DATETIME**—Date and time stamps enable the SQL procedure to determine the month, day, and year of a date as well the hour, minute, and second of a time.

See Chapter 5, “Creating, Populating, and Deleting Tables” and Chapter 6, “Modifying and Updating Tables” for more information about date and time informats and formats.

# Character Data

PROC SQL provides tools to manipulate and store character data including words, text, and codes using the CHARACTER or CHAR data type. The characters allowed by this data type include the ASCII or EBCDIC character sets. The CHARACTER or CHAR data type stores fixed-length character strings consisting of a maximum of 32K characters. If a length is not specified, a CHAR column stores a default of 8 characters.

The SQL programmer has a vast array of SQL and Base SAS functions that can make the task of working with character data considerably easier. In this chapter, you’ll learn how columns based on the character data type are defined, and how string functions, pattern matching, phonetic matching techniques, and a variety of other techniques are used with character data.

# Missing Values and NULL

Missing values are an important aspect when dealing with data. The concept of missing values is familiar to programmers, statisticians, researchers, and other SAS users. This chapter describes what NULL values are, what they aren’t, and how they are used.

Missing or unknown information is supported by PROC SQL in a form known as a *null value*. A null value is not the same as a zero value. In SAS, null values are treated as a separate category from known values. A value consisting of zero has a known value. In contrast, a value of null has an unknown quantity and will never be known. For example, a patient who is given an eye exam does not have zero eyesight just because the results from the exam haven’t been received. The correct value to assign in a case like this is a missing or a null value.

In another example, say a person declines to provide their age on a survey. This person’s age is null, not zero. Essentially, this person has an age, but it is unknown. Whenever an unknown value occurs, you have no choice but to assign an unknown value—null.