# Handling errors

Exception type information can be provided by including the C++ standard `<typeinfo>` library. Its `typeid()` function accepts an exception argument so its `name()` function can return the type name:

![](bbox=[0.12, 0.196, 0.2, 0.259])

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```
~~~cpp
#include <stdexcept> // Support standard exceptions.
#include <typeinfo> // Support type information.
#include <fstream>
#include <string>
#include <iostream>
using namespace std ;
~~~
```

+   2. Add a main function containing a final return statement, two initialized variable declarations, and a statement outputting a text message

```
~~~cpp
int main()
{
   string lang = "C++" ;
   int num = 1000000000 ; // One billion.
   // Try-catch block goes here.
   cout << "Program continues..." << endl ;
   return 0 ;
}
~~~
```

+   3. In the main function, insert a try block containing a statement attempting to replace part of the string value

```
~~~cpp
try { lang.replace( 100, 1 , "C" ) ; }
~~~
```

+   4. After the try block, add a catch block to handle a range exception then save, compile, and run the program

```
~~~cpp
catch( out_of_range &e )
{
   cerr << "Range Exception: " << e.what() << endl ;
   cerr << "Exception Type: " << typeid(e).name() ;
   cerr << endl << "Program terminated." << endl ;
   return -1 ;
}
~~~
```

![](bbox=[0.28, 0.7, 0.73, 0.758])

![](bbox=[0.12, 0.792, 0.21, 0.86])

The `out_of_range` error occurs because the `replace()` function is trying to begin erasing at the 100th character, but the `string` variable has only three characters.

+   5. Replace the statement in the try block with one attempting to resize the string variable

```
~~~cpp
lang.resize( 3 * num ) ;
~~~
```

+   6. After the catch block, add a second catch block to handle general exceptions