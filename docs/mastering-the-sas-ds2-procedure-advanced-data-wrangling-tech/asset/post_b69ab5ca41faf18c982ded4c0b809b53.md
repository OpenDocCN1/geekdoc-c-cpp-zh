
# Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

DS2 packages have no built-in mechanism for determining what methods are included in the package. In addition, to modify a single method, the entire package needs to be re-created. If you use DS2 packages—and I strongly encourage you to do so—you'll need some administrative controls in place to make them easier to use and administer. I would recommend some practices that can improve usability and make administration easier:

- Include a user-defined CONTENTS method in every package that you create. The CONTENTS method should not accept parameters. When called, this method should document the package in the SAS log. At a minimum, it should provide a list of the methods included in the package and the location of the source code. You will need to have the entire package source code to perform any maintenance on the package, as the whole package must be re-created each time a change is made.
- Every method in the package should be overloaded with a version of the method that accepts no parameters and does nothing but document the method in the SAS log.

Let's create a simple package that includes the two versions of our interest method and also includes the self-documenting features discussed above:

```
proc ds2;
package crs.MyMethods;
 contents();
  put 'This package contains the following methods:';
put '  - contents();';
put '  - interest();';
put;
  put 'Package source:';
put %tslit(&path);
put;
end;
method interest();
  put 'Syntax: interest(Amount,Rate,Years,Periods)>';
put '  Amount (double) - original amount';
put '  Rate (double) - interest rate';
put '  Years (int) - number of years for interest'
put '  yield();';
put '  Periods (int) - number of compounding periods';
put '  per year (optional)';
put;
  put 'If Periods are not specified, interest compounds annually;
  Returns total amount after compounding (double)';
put;
end;
method interest(double Amount, double Rate, int Years)
  returns double;
dcl int i;
do i=1 to Years;
  Amount=SUM(Amount,Amount*Rate);
end;
  return Amount;
end;
method interest(double Amount, double Rate, int Years
  , int Periods) returns double;
dcl int j;
do i=1 to Years;
do j=1 to Periods;
Amount=SUM(Amount, Amount*Rate/periods);
end;
return Amount;
endpackage;
run;
quit;
title:;
```

# SAS Log:

> NOTE: Created package mysymethods in data set cr.mysymethods.
NOTE: Execution succeeded. No rows affected.

If you are curious like me, you'll want to peek into the data set cr.mysymethods to see what a package looks like. Go ahead! As you can see in Figure 4, you'll find a little clear text header followed by a bunch of enchanted source code. Cool, but without interesting reading.

## Figure 4.4: Contents of the CRS.MyMethods Package

![](img/ef05c3db88dda150abd07414dd206d3f_75_0.png)

| SAS_ROWID_ | SAS_CHECKSUM | SAS_TEXTPACKAGE_ |
|---|---|---|
| 1 | 18122651414 | DATA_STEP_2_PROGRAM |
| 2 | 6098780327 | 1568 |
| 3 | 6687380327 | |
| 4 | 3029824840 | |
| 5 | 7189461221 | FTMTOEDANEVPE65EIA603MTPINGPESTVGUEQ4GOLLEINWRQ4LEJWTNT65 |
| 6 | 6450382472 | |
| 7 | 9017327308 | VALUHYGTEDK31ZFTGUE55CAKS55RP.INJ3DOYTGGUQOMSTGAHLQ |
| 8 | 42215452817 | KMWSKWMQJMDBLLGQUIBLFSJHYTYORZWCYZBHFTYROWCZNASNMMCC |
| 9 | 2693584753 | MKDXQRAQRVUON6JVAUHYODTSYBUXO5FBRC32ZXHWNRQ36O2FA2I |
| 10 | 7120110423 | HFEFUEIBVNFH63CAET33IN3IOOAS57K33INIOOAS57K33 |
| 11 | 2456580629 | GZJYTFTWEWKYGJMK32ZTDOB3QSTVEW7JHPBTGTZDTUTXLN4 |

## 4.3.2 Using Methods Stored in Packages

To use methods stored in a package, you will need to declare and instantiate an instance of the package. When you declare the package, you will give the instance an identifier. To use the methods in the package, simply call them using dot notation like instance.method().

A package is declared with a DCL PACKAGE statement and can be instantiated at compile time—that is, declared and instantiated at the same time. Alternatively, it can be instantiated at runtime—that is, declared first and then later in a separate executable statement. This is less complex. But if the package constructor method requires information that will not become available until the program begins executing, we would need to instantiate the package at run because the package we built didn't use parameters. We will see an example of this later.

Here's a program that uses the CONTENTS method from the package we created in the last section to determine what methods are available:

```
proc ds2;
data _null;
  /* Declare and instantiate the package */
  /* This instance's identifier is mm */
  dcl package crs.MyMethods mm();
  method init();
    /* Execute contents method from instance mm */
    mm.contents();
  end;
run;
```

ThisThis package contains the following methods:
- contents()
- interest()

Package source: DS2 Jumpstart

Next, we'll use the version of the INTEREST method without parameters to retrieve syntax for the INTEREST method:

```
proc ds2;
data _null;
  dcl package crs.MyMethods mm();
  method init();
    mm.interest();
  end;
run;
quit;
```

SAS Log:

Syntax: interest(Amount,Rate,Years,Periods)>
Amount (double) - original amount
Rate (double) - interest rate
Years (int) - number of years
Periods (int) - compounding periods/year (optional)

When periods are not specified, interest compounds annually Returns total amount after compounding (double)

Now that we know the syntax, let's use the INTEREST method to perform some work:

```
proc ds2;
title 'Results for each bank - initial $5000 deposit';
title 'compounding annually and daily ';data;
dcl package cr.MyMethods mm();
dcl double Total;
dcl int Periods;
keep Total Years bank;
method run();
Years=5;
Periods=1;
Total=mm.interest(5000,Rate,Years);
output;
Periods=365;
Total=mm.interest(5000,Rate,Years,Periods);
output;
enddata;
run;
quit;
title;
```

## Figure 4.5: Output from DS2 Program Using the Package Method
Results for each bank - initial $5,000 deposit compounding annually and daily

| | Years | Bank | |
|---|---|---|---|
| $5,847.20 | 5 | 1 | Carolina Bank and Trust | 0.318 |
| $5,861.65 | 5 | 365 | Carolina Bank and Trust | 0.318 |
| $5,855.70 | 5 | 1 | Big Federal Credit Union | 0.321 |
| $5,870.45 | 5 | 365 | Big Federal Credit Union | 0.321 |
| $5,875.59 | 5 | 1 | National Savings and Trust | 0.328 |
| $5,891.03 | 5 | 365 | National Savings and Trust | 0.328 |

## 4.3.3 Object-Oriented Programming with DS2 Packages

The ultimate power of the DS2 package comes from using it to enable object-oriented application design. In object-oriented programming, software objects can be used to model real-world objects, and existing objects can then be assembled to model other, more complex objects without having to re-write or re-test the existing objects' functionality. This can significantly speed up development cycles. For those who want to "kick it up a notch" with DS2 packages, we'll take a brief look at using packages as objects in a DS2 program.

You can think of a package as a "class": The package serves as the template from which an instance of object is created, and contains the necessary methods to create and destroy that instance, provide the object's behaviors (methods), and keep track of the object's current state (private global variables). For example, a household lamp. A lamp has functions (methods), such as operating its switch and its states—either on or off. In a DS2 package created to emulate a lamp, we would write methods to provide the lamp's function and create package variables to keep track of the lamp's status.

Although packages cannot include the automatically executed system methods INIT, RUN, and TERM, each package includes two special methods called the constructor and destructor. Constructor and destructor methods do not return types and cannot return values.

The destructor method is always DELETE and is automatically generated by the DS2 package program. It performs cleanup and releases packages back to the system whenever a package is terminated (destroyed). You can write your own DELETE method to add custom routines. The DELETE method executes automatically whenever a package instance goes out of scope and destroyed.
