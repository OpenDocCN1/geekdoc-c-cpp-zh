# You Do It

# Calling a Method

In this section, you write a program in which a Main() method calls another method that displays a company's logo.

+   1. Open a new program named DemoLogo, and enter the statement that allows the program to use System.Console methods without qualifying them. Then type the class header for the DemoLogo class and the class-opening brace.

   using static System.Console;
   class DemoLogo
   {}

+   2. Type the Main() method for the DemoLogo class. This method displays a line, then calls the DisplayCompanyLogo() method.

   static void Main()
   {
      Write("Our company is ");
      DisplayCompanyLogo();
   }

+   3. Add a method that displays a two-line logo for a company.
   private static void DisplayCompanyLogo()
   {
      WriteLine("See Sharp Optical");
      WriteLine("We prize your eyes");
   }

+   4. Add the closing curly brace for the class { } }, and then save the file.

+   5. Compile and execute the program. The output should look like Figure 7-7.

```
Our company is See Sharp Optical
We prize your eyes
```

Figure 7-7 Output of the DemoLogo program

(continues)