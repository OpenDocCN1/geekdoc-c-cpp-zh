# LISTING 2.9 continued

```
{
    int miles;
    double gallons, mpg;

    Scanner scan = new Scanner (System.in);

    System.out.print ("Enter the number of miles: ");
    miles = scan.nextInt();

    System.out.print ("Enter the gallons of fuel used: ");
    gallons = scan.nextDouble();

    mpg = miles / gallons;

    System.out.println ("Miles Per Gallon: " + mpg);
}
```

# OUTPUT

Enter the number of miles: 328
Enter the gallons of fuel used: 11.2
Miles Per Gallon: 29.28571428571429

A Scanner object processes the input one token at a time, based on the methods used to read the data and the delimiters used to separate the input values. Therefore, multiple values can be put on the same line of input or can be separated over multiple lines, as appropriate for the situation.

In Chapter 5 we use the Scanner class to read input from a data file and modify the delimiters it uses to parse the data. Appendix H explores how to use the Scanner class to analyze its input using patterns called regular expressions.

VideoNote
Example using the Scanner class.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 2.36 Identify which line of the GasMileage program does each of the following.

+   a. Tells the program that we will be using the Scanner class.
+   b. Creates a Scanner object.
+   c. Sets up the Scanner object scan to read from the standard input stream.
+   d. Reads an integer from the standard input stream.