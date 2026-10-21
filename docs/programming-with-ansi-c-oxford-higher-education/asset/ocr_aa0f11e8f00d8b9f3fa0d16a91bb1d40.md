# PROGRAM 13.6 Swap two records of a file

```
```cpp
//SwapRecords.cpp
#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>
using namespace std;

class customer
{
	int CustId;
	string Name;
public:
	customer()
	{
		CustId = 0;
		Name = "Dummy";
	}

	customer(int TempCustId, string TempName)
	{
		CustId = TempCustId;
		Name = TempName;
	}

	friend operator <<(ostream TempOut, customer TempCustomer)
	{
		TempOut << TempCustomer.CustId << " " << TempCustomer.Name << endl;
	}
};

int main()
{
	fstream CustomerFile("Cust.dat", ios::in | ios::out | ios::trunc | ios::binary);
	/* Opening customer file in binary mode; trunc ensures deletion of file if exists */
	customer Lara(1, "Brian Charles Lara");
	customer Beckham(2, "David Beckham");
	customer Steffh(3, "Steffi Graf");
	/* Three customer objects are defined */
	customer Answer1, Answer2;
	CustomerFile.write((char *)&Lara, sizeof(Lara));
	CustomerFile.write((char *)&Beckham, sizeof(Beckham));
	CustomerFile.write((char *)&Steffh, sizeof(Steffh));
	/* sizeof operator can be applied to both a class and an object; so, sizeof(customer) and sizeof(Beckham) yield the same value */
	cout << "Record no. 1 is as follows: \n";
	CustomerFile.seekg(0, ios::beg);
	/* Reaching the beginning of the file */
	if(!CustomerFile.read((char *)&Answer1, sizeof(customer)))
		cout << "Error in reading file";
	/* Reading the customer record from file */
	cout << Answer1;
	/* Writing the record on the screen */
	cout << "Record no. 3 is as follows: \n";
```
```