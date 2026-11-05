The try...catch statement is used to catch exceptions that occur during execution of a block, and the try...finally statement is used to specify finalization code that is always executed, whether an exception occurred or not.

The checked and unchecked statements are used to control the overflow checking context for integral-type arithmetic operations and conversions.

The lock statement is used to obtain the mutual-exclusion lock for a given object, execute a statement, and then release the lock.

The using statement is used to obtain a resource, execute a statement, and then dispose of that resource.

The following table lists C#'s statements and provides an example for each one.

| Statement | Example |
|---|---|
| Local variable declaration | static void Main() { 
  int a;
  int b = 2, c = 3;
  a = 1;
  Console.WriteLine(a + b + c);
} |
| Local constant declaration | static void Main() { 
  const float pi = 3.1415927f;
  const int r = 25;
  Console.WriteLine(pi * r * r);
} |
| Expression statement | static void Main() { 
  int i;
  i = 123; // Expression statement
  Console.WriteLine(i); // Expression statement
  i++; // Expression statement
  Console.WriteLine(i); // Expression statement
} |
| if statement | static void Main(string[] args) { 
  if (args.Length == 0) {
    Console.WriteLine("No arguments");
  } else {
    Console.WriteLine("One or more arguments");
  }
} |