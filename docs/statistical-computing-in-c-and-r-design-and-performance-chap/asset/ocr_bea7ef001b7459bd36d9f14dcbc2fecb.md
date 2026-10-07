# 58 A SKETCH OF C++

```
double Power::xToTheK(double x){
  double y = 1;
  for(int i = 1; i <= K; i++)
    y = x*y;
  return y;
}
```

Note that an include directive has been used to bring in the Power class prototype contained in Class.h. The use of quotation marks instead of < > tells the preprocessor to begin looking for the header file in the current directory.

Finally, a program that actually uses class Power

```
//powerClassDriver.cpp
#include <iostream>
#include "powerClass.h"

using namespace std;

int main(){
  int k;
  double x;
  cout << "Enter an integer power ";
  cin >> k;
  Power powObj(k);
  cout << "Enter a number to raise to this power ";
  cin >> x;
  cout << powObj.xToTheK(x) << endl;
  return 0;
}
```

Observe that the header file for class Power has been included in this driver program and that a Power object is now being used to call the xToTheK method.

In looking back at the header file and associated cpp file for class Power, one will see that the namespace directive was only employed in the cpp file. This was done for purpose and it is, in general, not place namespace directives in header files. The reason for this is that the preprocessor inserts the content of a header file into any source file (which could be another header file) that imports it via #include statement. This means that a namespace designation in a header file can propagate unintentionally if the header is being used several times in a multiple source code project. The result can be name clashes that are hard to diagnose. Therefore, it is best to use explicit namespace qualifiers via the scope resolution operator in header files and restrict the use of namespace directives to the cpp files for a class. We will demonstrate this in the next section.

The only thing remains is showing how to create an executable program using three separate files for the code. This can be accomplished directly via

```
$ g++ -Wall powerClass.cpp powerClassDriver.cpp -o powerClass
./powerClass
Enter an integer power 3
Enter a number to raise to this power 1.2
1.728
```

which is a direct extension to use the -c option of the GNU compiler to create intermediate object files of our previous approach to compilation. Alternatively, one can use