# Chapter 17 Input, Output, and Files

```
{
  cout << bf.what() << endl;
  cout << "O! the horror!\n";
}
```

```
cout << "Last value entered = " << input << endl;
cout << "Sum = " << sum << endl;
return 0;
```

Enter a sample run of the program in Listing 17.12: the what() depends on the implementation:

Enter numbers: 20 30 40 pi 6
ios_base failure in clear
O! the horror!
Last value entered = 40.00
Sum = 90.00

So that you can use exceptions for input. But should you use them? It depends on the context. For this example, the answer is no. An exception should catch an unusual, unexpected occurrence, but this particular program would use a mismatch as the way to exit the loop. It might make sense, however, for a program to throw an exception for bad because that circumstance would be unexpected. Or if the program were designed to read numbers from a data file up to end-of-file, it might make sense to throw an exception for failbit that would represent a problem with the data file.

# Stream State Effects

An if or while test such the following tests as true only if the stream state is good (all bits cleared):

```
while (cin >> input)
```

If a test fails, you can use the member functions in Table 17.4 to discriminate among possible causes. For example, you could modify the central part of Listing 17.11 to look like this:

```
while (cin >> input)
{
  sum += input;
}
if (cin.eof()) {
  cout << "Loop terminated because EOF encountered\n";
```

Setting a state bit has a very important consequence:The stream is closed for further input or output until the bit is cleared. For example, the following code won not:

```
while (cin >> input)
{
```