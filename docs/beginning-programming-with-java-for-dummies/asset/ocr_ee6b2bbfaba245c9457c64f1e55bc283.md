# Math

Do you have any numbers to crunch? Do you use your computer to do exotic calculations? If so, try Java’s Math class. (It’s a piece of code, not a place to sit down and listen to lectures about algebra.) The Math class deals with π, e, logarithms, trig functions, square roots, and all those other mathematical things that give most people the creeps.

# NumberFormat

Chapter 18 has a section about the NumberFormat.getCurrencyInstance method. With this method, you can turn 20.33850000000003 into $20.34. If the United States isn’t your home, or if your company sells products worldwide, you can enhance your currency instance with a Java Locale. For example, with euro = NumberFormat.getCurrencyInstance(Locale.FRANCE), a call to euro.format(3) returns 3,00 € instead of $3.00.

The NumberFormat class also has methods for displaying things that aren’t currency amounts. For example, you can display a number with or without commas, with or without leading zeros, and with as many digits beyond the decimal point as you care to include.

# Scanner

Java’s Scanner class can do more than what it does in this book’s examples. Like the NumberFormat class, the Scanner can handle numbers from various locales. For example, to input 3,5 and have it mean “three and half,” you can type myScanner.useLocale(Locale.FRANCE). You can also tell a Scanner to skip certain input strings or use numeric bases other than 10. All in all, the Scanner class is very versatile.

# String

Chapter 18 examines Java’s String class. The chapter describes (in gory detail) a method named equals. The String class has many other useful methods. For example, with the length method, you find the number of