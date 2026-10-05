representation of the date. Remember, the value of the year field represents year + 1900, and the value of the day field represents day + 1.

> Note
nThe ToString method is a little different from the methods you've seen so far. Every type, including structures and classes that you define, automatically has a ToString method whether you want it or not. Its default behavior is to convert the data in a variable to a string representation of data. Sometimes the default behavior is meaningful; other times it is less so. For example, the default behavior of the ToString method generated for the Date structure simply generates the string StructsAndEnums. Quote Zaphod Beeblebrock in The Restaurant at the End of the Universe by Douglas Adams (Pan Macmillan, 1980), this is “shrewd, dull.” You need to define a new version of this method that overrides the default behavior by using the override keyword. The topic of overriding methods is discussed in more detail in Chapter 12.

The ToString method should look like this:

Click here to view code image

In this method, you build a formatted string using the text representations of the values of the month field, the expression this.day + 1, and the