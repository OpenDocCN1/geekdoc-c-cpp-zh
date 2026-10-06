# Example 121 Nested for Loops to Print a Triangle of Asterisks

```
for (int i=1; i<=4; i++) {      // Output:
    for (int j=1; j<=i; j++) {           // *
        Console.Write("*");\                // **
        Console.WriteLine();               // ***
    }                               // ****
```

# Example 122 Multiple Initialization and Step in a Loop

This method reverses the elements of a one-dimensional array. Note the multiple variable declarations in the initialization and the multiple (comma-separated) expressions in the step part of the loop header.

```
public static void Reverse(Object[] arr) {
    for (int s=0, t=arr.Length-1; s<t; s++, t--) {
        Object temp = arr[s]; arr[s] = arr[t]; arr[t] = temp;
    }
}
```

# Example 123 Using foreach on an Array

This loop concatenates the strings in the array arr, inserting two copies of each string. The binding of an element to local variable s in the foreach loop involves an implicit conversion to type String, so the example will compile and execute regardless of whether the type of arr is String[] or Object.

```
StringBuilder sb = new StringBuilder();
foreach (String s in arr) {
    sb.Append(s).Append(s);
}
```

# Example 124 Explicitly Using an IEnumerator instead of foreach

A foreach loop in example 123 is sugar for a while loop using an enumerator. Note the explicit conversion to String; in the foreach statement it is invisible but nevertheless performed. If the loop body were to terminate abruptly by a return statement, the finally block would call the enumerator's Dispose method if it has, so the enumerator can immediately free any resources it holds on. The IDisposable interface is described in section 13.10.

```
StringBuilder sb = new StringBuilder();
IEnumerator enm = arr.GetEnumerator();
try {
    while (enem.MoveNext()) {
        String s = (String)enem.Current;
        sb.Append(s).Append(s);
    }
} finally {
    Console.WriteLine("now in finally block");
    IDisposable disp = enm as System.IDisposable;
    if (disp != null)
        disp.Dispose();
}
```