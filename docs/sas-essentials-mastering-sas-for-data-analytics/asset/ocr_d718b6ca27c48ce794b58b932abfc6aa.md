24 CHAPTER 2: GETTING DATA INTO SAS®

# 2.4 UNDERSTANDING SAS VARIABLE TYPES

SAS is designed to differentiate among three basic types of variables: numeric, text, and date.

+   * Numeric Variables (Default): A numeric variable is used to designate values that could be used in arithmetic calculations or are grouping codes for categorical variables. For example, the variables SBP (systolic blood pressure), AGE, and WEIGHT are used. However, an ID number, phone number, or Social Security number should not be designated as a numeric variable. For one thing, you typically not want to use them in a calculation. Moreover, for ID numbers, if ID = 00012 was stored as a number, it would lose the zeros and become 12.
* Character (Text, String) Variables: Character variables are used for values that are not used in arithmetic calculations. For example, a variables M and F are codes for gender a character variable. For character variables, case matters, because the computer considers lowercase f different from uppercase F. It is important to note that a character variable may contain numerical digits. As mentioned previously, a Social Security number (e.g., 450-67-7823) or an ID number (e.g., 04321) should be designated as a character variable because their values should never be used in mathematical calculations. When designating a character variable in SAS, you must indicate to SAS that it is of character type. This is shown in upcoming examples.
* Date Variables: A date value may be entered into SAS using a variety of formats, such as 10/15/09, 01/05/2010, JAN052010, and so on. As you will see in upcoming examples, dates are handled in SAS format specifications that tell SAS how to read or display the date values. For more information about dates in SAS, see Appendix B.

# 2.5 METHODS OF READING DATA INTO SAS

The following sections illustrate several techniques for entering data (creating a data set) in SAS. These are not the only ways to enter data into SAS, but they are the most common. The methods discussed are as follows:

+   * Reading data freeform list input
* Reading data the compact method
* Reading data using column input
* Reading data formatted input.

Methods of importing data from other file formats (such as Excel) are discussed in the following chapter. Moreover, the initial examples of these data entry methods illustrate how to read data that are within the SAS code; but these methods can also be used to read data from an external file, as will be illustrated later.

# 2.5.1 Reading Data Using Freeform List Input

A simple way to enter data into SAS is as freeform input. In this method, variable names in the DATA step are indicated by a list following the INPUT statement keyword. For example: