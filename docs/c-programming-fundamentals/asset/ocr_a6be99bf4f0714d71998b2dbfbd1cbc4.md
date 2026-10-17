**d.** Inside try  
Exception Caught  
After throw  
After catch

# 31. What is the output of this program?

```
```cpp
#include<iostream>
using namespace std;
int main ()
{
try {
int* myarray = new int[1000];
cout << "Allocated";
}
catch (exception& LFC){
cout << "Standard exception: " << LFC.what() << endl;
}
return 0;
}
```
```

+   a. Error  
+   
+   b. Allocated  
+   
+   c. Standard exception  
+   
+   d. Depends on the memory

# 32. What is the output of the following C++ code?

```
```cpp
#include <iostream>
using namespace std;
int main()
{
    try
    {
        try
        {
            throw 20;
        }
        catch (int n)
        {
            cout << "Inner Catch\n";
        }
    }
    catch (int x)
```
```