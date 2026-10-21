# # Operator Overloading and User-defined Conversions 267

```
index++;
else if(Choice == 2)
{
	for(int i = 0; i < index; ++i)
	{
		/* The conversion takes place here */
		string NameOfUser = *ArrayOfUsers[i];
		/* One of the following could also be used instead */
		cout << (string)*ArrayOfUsers[i] << "\n";
		cout << string(*ArrayOfUsers[i]) << "\n";
		/* In both the cases, the conversion is done with the help of typecasting. The first case is C-style casting whereas the next one is a newer cast available in C++ */
		cout << NameOfUser;
	}
}
else
exit(0);
}
```



We will only look at the code that converts the object into a built-in type value. String is considered to be a built-in type in the following. In a strict sense, it is not built in but is a part of Standard Template Library (STL).



In the following statement string NameOfUser = *ArrayOfUsers[i]; we have assigned the object to a string. It is acceptable to the compiler because we have written a conversion function. The conversion function itself is very simple. Let us look at it again.

```
operator string()
{
	return Name;
}
```

The other two statements that perform a similar conversion are as follows:

cout << (string)*ArrayOfUsers[i] << "\n";
cout << string(*ArrayOfUsers[i]) << "\n";

This function converts the object of type LoggedInUser to a string. It tells the compiler to convert LoggedInUser to a string, and then copy the Name value of LoggedInUser to the string.



Though we have not specified, we are returning an object of type string in the operator function. We cannot specify a return type in the header of an operator function. The syntax of a header is as follows:

```
operator <built-in type name>()
```