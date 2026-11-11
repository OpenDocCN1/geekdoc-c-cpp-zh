# ■ Creating Dynamic Constructors

The constructors that can allocate the required amount of memory to objects at the time of their construction are known as dynamic constructors of objects. The memory is allocated with the help of the `new` operator. Listing 18 shows how to call dynamic constructors (you can find this example in the DynamicConstructor.cpp file on the CD in the `code\chapter6` folder):

# ▶ Listing 18: Calling Dynamic Constructors

```
```cpp
#include <iostream.h>

class AddingNumbers
{
  int *numPoint;
  int numSize;

public:
  AddingNumbers (int size)
  {
    numSize = size;
    numPoint = new int[size];
  }
  ~AddingNumbers ()
  {
    delete numPoint;
  }
  void input();
  void additionDisplay();
};

void AddingNumbers::input()
{
  for( int i = 0; i < numSize; i++ )
  {
    cout << "Enter a number at the position [ " << i << " ] ? ";
    cin >> numPoint [i];
  }
}
void AddingNumbers::additionDisplay()
{
  int sum=0;
  for( int i = 0; i < numSize; i++ )
    sum += numPoint [i];
  cout << "Sum of the numbers = " << sum;
}
void main()
{
  int num;
```
```