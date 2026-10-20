# Defining Constants

Constants are fixed values in your code. They can be any basic data type but as the name suggests their value remains constant throughout the entire code. There are two separate ways to define a constant in C++, the #define pre-processor and const.

# #DEFINE

The pre-processors are instructions to the compiler to pre-process the information before it goes ahead and compiles the code. #include is a pre-processor as is #define.

STEP 1 You can use the #define pre-processor to define any constants you want in our code. Start by creating a new C++ file complete with the usual headers:

```
#include <iostream>
using namespace std;

int main ()
{
}
```

![](bbox=[0.07, 0.51, 0.49, 0.62])

STEP 3 Note the capitals for defined constants, it's considered good programming practise to define all constants in capitals. Here, the assigned values are 50, 40 and 60, so let's call them up:

```
#include <iostream>
using namespace std;

#define LENGTH 50
#define WIDTH 40
#define HEIGHT 60

int main ()
{
    cout << "Length is: " << LENGTH << "\n";
    cout << "Width is: " << WIDTH << "\n";
    cout << "Height is: " << HEIGHT << "\n";
}
```

![](bbox=[0.52, 0.6, 0.93, 0.79])

STEP 2 Now let's assume your code has three different constants: length, width and height. You can define them with:

```
#include <iostream>
using namespace std;
#define LENGTH 50
#define WIDTH 40
#define HEIGHT 60

int main ()
{
}
```

![](bbox=[0.07, 0.82, 0.49, 0.95])

STEP 4 Build and run the code. Just as expected, it displays the values for each of the constants created. It's worth noting that you don't need a semicolon when you're defining a constant with the #define keyword.

![](bbox=[0.52, 0.87, 0.93, 0.95])