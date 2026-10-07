# Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

DS2 packages have no built-in mechanism for determining what methods are included in the package. In addition, to modify a single method, the entire package needs to be re-created. If you use DS2 packages—and I strongly encourage you to do so—you'll need some administrative controls in place to make them easier to use and administer. I would recommend some practices that can improve usability and make administration easier:

+   - Include a user-defined CONTENTS method in every package that you create. The CONTENTS method should not accept parameters. When called, this method should document the package in the SAS log. At a minimum, it should provide a list of the methods included in the package and the location of the source code. You will need to have the entire package source code to perform any maintenance on the package, as the whole package must be re-created each time a change is made.
- Every method in the package should be overloaded with a version of the method that accepts no parameters and does nothing but document the method in the SAS log.

Let's create a simple package that includes the two versions of our interest method and also includes the self-documenting features discussed above:

```
proc ds2;
package crs.MyMethods;
 contents();
put;
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
decl int i;
do i=1 to Years;
  Amount=SUM(Amount,Amount*Rate);
end;
  return Amount;
end;
method interest(double Amount, double Rate, int Years
  , int Periods) returns double;
```