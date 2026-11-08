```
~~~cpp
cout << "Enter a two digit number: ";
cin >> num;
cout << endl;

id = 100 * num + SECRET;

cout << "Enter a positive integer less than 1000: ";
cin >> num;
cout << endl;

mysteryNum = num * PRIME_NUM - 3 * SECRET;

cout << "Name: " << name << endl;
cout << "Id: " << id << endl;
cout << "Mystery number: " << mysteryNum << endl;

return 0;
}
~~~
```

33. Rewrite the following program so that it is properly formatted.

```
~~~cpp
#include <iostream>
#include <string>
using namespace std;
const double X = 13.45; const int Y=34;
const char BLANK= ' ';
int main()
{ string firstName,lastName;int num;
  double salary;
  cout<<"Enter first name: "; cin>> firstName; cout<<endl;
  cout<<"Enter last name: "; cin
  >>lastName;cout<<endl;
      cout<<"Enter a positive integer less than 70:";
  cin>>num;cout<<endl; salary=num*X;
  cout<<"Name: "<<firstName<<BLANK<<lastName<<endl;cout
  <<"Wages: $"<<salary<<endl; cout<<"X = "<<X<<endl;
  cout<<"X+Y = " << X+Y << endl; return 0;
}
~~~
```

34. What type of input does the following program require, and in what order does the input need to be provided?

```
~~~cpp
#include <iostream>

using namespace std;

int main()
{
    int invoiceNumber;
    double salesTaxRate;
    double productPrice;
    string productName;
~~~
```