# Exception Handling 355

```
void ExGen() throw()
{
	cout << "Inside the function \n";
	cout << "Inside try block \n";
	cout << "Assuming error and throwing exception now \n";
	MyException Error1(20, "Error testing");
	throw Error1;
	cout << "This statement will not be executed";
}

void MyUnExpected()
{
	cout << "This is my unexpected function \n";
	/* The cleanup code comes here; it closes all open files, closes open connections, and runs destructors if needed */
	exit(-1);
}

int main()
{
	try
	{
		void MyUnExpected();
		set_unexpected(MyUnExpected);
		cout << "Inside main\n";
		ExGen();
		// This would generate an exception for which no catch is available
		cout << "This will not be executed \n";
	}
	catch(...)
	{
		cout << "Caught it!";
	}
	return 0;
}
```



```
Inside main
Inside the function
Inside the function
Inside try block
Inside try block
Assuming error and throwing exception now
This is my unexpected function
```

The function ExGen() has exception specification as throw(). If ExGen() throws some exception, the unexpected() function would be called and the output of this function is "This is my unexpected function". In the given example, we have written our own function for