```
{
cout<<"\n memory insufficient";
exit(1);
}
void*operator new(size_t s, int v)
{
void*c;
c=malloc(s);
if(c==null)
{
message();
memset(c,v,s);
return c;
}
}
void operator delete(void*dd)
{
free(dd);
}
```

```
Output
First time memory allocation:p=3267
$$$$$$$$$$
Memory insufficient.
```

In Program 1.27, the new and delete operators are overloaded. The size_t is used to define the size of the object. The message() is called by the new operator when the malloc() function returns null. The new operator fails to allocate memory and calls the function message(), when the statement c=new( * ) char[4000ul] requests memory allocation. The delete operator releases memory when called by using free().

# 1.10 EXCEPTION HANDLING

Any mistake in writing the program results in an error, errors are of two types—syntax errors and semantic errors. The exception handling mechanism is used to reduce such errors. Exception is an error that occurs at runtime and the program terminates due to the exception. Exceptions are of two types—synchronous and asynchronous exceptions.

The exception handling mechanism detects the exception, intimates that the exception occurred, receives the error message and takes necessary actions without disturbing the users. The exception handling mechanism involves three keywords, try, catch, throw.

Whenever an exception occurs, the control passes from the point of exception to the exception handler, which is linked with the try block and is called only by the throw statement. The general form of try, catch and throw is as follows.

```
try
{
Statement 1:       //try block
Statement 2;
}
```