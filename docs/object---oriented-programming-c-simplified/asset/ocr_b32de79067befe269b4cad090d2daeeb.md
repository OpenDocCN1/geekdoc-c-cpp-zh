```
/*PROG 14.14 RE-THROWING AN EXCEPTION VER 2 */
#include <iostream.h>
#include <math.h>
void main()
{
	void check(int x);
	int x;
	cout << "Enter a +ve number \n";
	cin >> x;
	try
	{
		check(x);
	}
	catch(char*s)
	{
		cout << "Exception thrown in main \n";
		cout << s << endl;
	}
	cout << "Terminating main \n";
}
void check(int x)
{
	char*str="cannot take square root of -ve numbers \n";
	try
	{
		if(x<0)
			throw str;
		else
			cout << "square root is " << sqrt(x) << endl;
	}
	catch(char*)
	{
		cout << "Caught exception in function\n";
		cout << "Rethrowing \n";
		throw;
	}
}
```