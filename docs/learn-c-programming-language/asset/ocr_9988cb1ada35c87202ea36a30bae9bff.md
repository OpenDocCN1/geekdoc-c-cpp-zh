```
```cpp
{
    cout << "D2 is less than D1 " << endl;
}
return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```text
D2 is less than D1
```
```

# Input/Output Operators Overloading

C++ is able to input and output the built-in data types using the stream extraction operator >> and the stream insertion operator <<. The stream insertion and stream extraction operators also can be overloaded to perform input and output for user-defined types like an object.

Here, it is important to make operator overloading function a friend of the class because it would be called without creating an object.

Following example explains how extraction operator >> and insertion operator <<.

```
```cpp
#include <iostream>

using namespace std;

class Distance
{
    private:
        int feet;             // 0 to infinite
        int inches;           // 0 to 12
    public:
        // required constructors
        Distance(){
            feet = 0;
            inches = 0;
        }
        Distance(int f, int i){
            feet = f;
            inches = i;
```
```