# Object-Oriented Programming C++ Simplified

```
public :

void input( )
{
	cout << "ENTER A STRING :=";
	cin >> str;
}

void find_len( )
{
	int i=0;
	while(str[i++]!=0);
	len =i;
}

void show( )
{
	cout << "String :=" << str << endl;
	cout << "Length :=" << len << endl;
}
};

void main( )
{
	demo_str str;
	clrscr( );
	str.input( );
	str.find_len( );
	str.show( );
	getch( );
}
```

OUTPUT :

ENTER A STRING :=Hari Mohan

String :=Hari

Length :=5

A string is nothing but an array of character terminated by null character `\0`. We have three function input, find_len and show. The function input takes input from the user and store the string in the variable str. The function find_len finds the length of the string control variable i, till str[i]!=0. The body of the while loop is simple the null statement. In the end when loop terminates ` ` is assigned to len. Through show we display str and len. From the output you can conclude that cin stops at the very first white space character and "hari" including space where it stopped is assigned to str.