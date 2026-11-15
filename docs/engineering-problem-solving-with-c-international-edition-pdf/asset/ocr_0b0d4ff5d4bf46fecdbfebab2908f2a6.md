![](bbox=[0.135, 0.09, 0.205, 0.135])

![](bbox=[0.135, 0.145, 0.205, 0.19])

The keyword `template`, followed by a parameter list enclosed within <> symbols, must precede a function template definition and a function template prototype. Within the parameter list the keyword `typename` precedes each identifier in the list, indicating that the identifier represents a data type. The template parameter list must include at least one parameter. If multiple parameters are used, they are separated with commas, as in:

```
template <typename T1, typename T2, typename T3>
```

The following program calls the function template `minVal()` four times to find the smallest value in arrays of type `int`, `char`, `double`, and `string`.

```
/*--------------------------------------------------------------*
| Program chapter10_1                                          |
|                                                              |
| This program demonstrates the use of the function            |
| template minVal.                                             |
*--------------------------------------------------------------*/
#include<iostream> //Required for cout.
#include<string> //Required for string.
using namespace std;
//Function Prototype
template <typename Dtype>
Dtype minVal(const Dtype x[], int n);
int main()
{
 //Declare objects.
 const int SIZE = 10;
 char ch[SIZE] = {'h','e','l','l','o',' ','w','o','r','l','d'};
 int idat[SIZE] = {5,2,7,8,2,5,9,8,1,9};
 double ddat[SIZE] = { -2.1,4.3,0.0,9.3,0.4,-4.2};
 string sdat[SIZE] = {"this","short","the","list","of","strings"};
 //Print smallest value in each array.
 cout << "\nSmallest value in ch array."
 << "\n" << minVal(ch,SIZE) << endl; // Char
 cout << "\nSmallest integer in idat is "
 << minVal(idat,SIZE) << endl; // int
 cout << "\nSmallest double in ddat is "
 << minVal(ddat,6) << endl; // double
 cout << "\nSmallest string in sdat is "
 << minVal(sdat,6) << endl; // string
 return 0;
}
/*--------------------------------------------------------------*/
```