+   (a) No error
+   (b) Termination occurs
+   (c) Unexpected behavior
+   (d) Throws invalid_cast exception

**Answer:** (a) No error

**33.** Which of these keywords is used to re-throw a caught exception? (L1)

+   (a) Throw
+   (b) Rethrow
+   (c) finally
+   (d) catch(...)

**Answer:** (a) Throw

**34.** C++ throws exceptions which are of which kind among the following? (L1)

+   (a) Checked
+   (b) Unchecked

**Answer:** (b) Unchecked. In C++, all the exceptions are unchecked. They are not checked by the compiler during compile time. It is the programmers’ responsibility to take care of situations.

**35.** Say Yes or No: Can we nest try-catch blocks in a C++ program? (L1)

+   (a) Yes
+   (b) No

**Answer:** (a) Yes

**36.** Divide by zero error has to be handled by the programmers themselves. Say true or false. (L1)

+   (a) True
+   (b) False

**Answer:** (a) True. `std::overflow_error` has to be thrown after checking if the denominator is zero.

**37.** Predict the output of the following program. (L2)

```
#include <iostream>
#include <string>
#include <typeinfo>
#include <stdexcept>
using namespace std;

int main( )
{
try
{
```

```
cout<<"Outside try"<<endl;
try
{
int numerator = 10, denominator =0;
if(denominator==0)
throw std::runtime_error("Divide by zero exception occurred");
else
cout<<numerator/denominator;
}
catch(std::overflow_error& e)
{
cout<<"inner catch"<<endl<<e.what()<<endl;
throw;
}
}
catch (...)
{
cout<<"outer catch"<<endl;
};
return 0;
}
```

+   (a) Outside try; after this, the program terminates
+   (b) Outside try
+       Inner catch
+       Divide by zero exception occurred
+       Outer catch
+   (c) Outside try
+       Outer catch
+       Inner catch
+       Divide by zero exception occurred
+   (d) Compile time error occurs

**Answer:** (b)

**38.** Choose the exception which is not handled by C++ program? (L1)

+   (a) Out of range exception
+   (b) Memory overflow exception
+   (c) Keyboard interrupts
+   (d) Invalid cast exception