# # 630 Object-Oriented Programming C++ Simplified

```
```cpp
n1 = x;
n2 = y;
show();
}
void show ()
{
	cout << n1 << " is of type " << typeid(int).name() << endl;
	cout << n2 << " is of type " << typeid(float).name() << endl;
}
```

```
```cpp
/* PROG 13.15 CLASS TEMPLATE FOR FINDING SUM OF ARRAY ELEMENTS */
#include <iostream.h>
#include <typeinfo.h>
#define S 5
template <class TARR>
class demo
{
	TARR arr[S];
	public :
	demo()
	{
		int i;
		cout << "Enter " << S << " " << typeid(TARR).name() << " numbers\n";
		for(i=0;i<S;i++)
			cin >> arr[i];
	}
	TARR sum()
	{
		int i;
		TARR s=0;
		for(i=0;i<S;i++)
			s += arr[i];
		return s;
	}
};
```