
# Example 121 Nested for Loops to Print a Triangle of Asterisks

```csharp
for (int i=1; i<=4; i++) {      // Output:
    for (int j=1; j<=i; j++) {           // *
        Console.Write("*");                // **
        Console.WriteLine();               // ***
    }                               // ****
```

# Example 122 Multiple Initialization and Step in a Loop

This method reverses the elements of a one-dimensional array. Note the multiple variable declarations in the initialization and the multiple (comma-separated) expressions in the step part of the loop header.

```csharp
public static void Reverse(Object[] arr) {
    for (int s=0, t=arr.Length-1; s<t; s++, t--) {
        Object temp = arr[s]; arr[s] = arr[t]; arr[t] = temp;
    }
}
```

# Example 123 Using foreach on an Array

This loop concatenates the strings in the array arr, inserting two copies of each string. The binding of an element to local variable s in the foreach loop involves an implicit conversion to type String, so the example will compile and execute regardless of whether the type of arr is String[] or Object.

```csharp
StringBuilder sb = new StringBuilder();
foreach (String s in arr) {
    sb.Append(s).Append(s);
}
```

# Example 124 Explicitly Using an IEnumerator instead of foreach

A foreach loop in example 123 is sugar for a while loop using an enumerator. Note the explicit conversion to String; in the foreach statement it is invisible but nevertheless performed. If the loop body were to terminate abruptly by a return statement, the finally block would call the enumerator's Dispose method if it has, so the enumerator can immediately free any resources it holds on. The IDisposable interface is described in section 13.10.

```csharp
StringBuilder sb = new StringBuilder();
IEnumerator enm = arr.GetEnumerator();
try {
    while (enm.MoveNext()) {
        String s = (String)enm.Current;
        sb.Append(s).Append(s);
    }
} finally {
    Console.WriteLine("now in finally block");
    IDisposable disp = enm as System.IDisposable;
    if (disp != null)
        disp.Dispose();
}
```

## 13.6.3 The while Statement

A while statement has the form

```csharp
while (condition)
  body
```

where the *condition* is an expression of type bool, and *body* is a statement but not a declaration statement or a labeled statement. The while statement is executed as follows:

- 1. The *condition* is evaluated. If it is false, the loop terminates.
- 2. If it is true, then
  (a) the *body* is executed;
  (b) execution continues at 1.

An infinite loop can be written *while (true) body*, which may be clearer than the “forever” idiom for (;;) *body* shown in 13.6.1.

## 13.6.4 The do–while Statement

A do–while statement has the form

```csharp
do
  while (condition);
```

where *condition* is an expression of type bool, and *body* is a statement but not a declaration statement or a labeled statement. The do-while statement is executed as follows:

- 1. The *body* is executed.
- 2. The *condition* is evaluated. If it is false, the loop terminates.
- 3. If it is true, execution continues at 1.

The body is always executed at least once because the *condition* is tested only after executing the *body*. This also means that the *condition* does not contribute to establishing a precondition that guarantees successful execution of the *body*. Usually it is safer and more appropriate to use a while loop or for loop, which do test the *condition* before executing the *body*.

## Example 125 Array Search Using a while Loop

This method converts a weekday (Thursday, say) into a day number (4, say), by searching an array of weekday names. Note that after the while loop, the negation of the loop condition holds. Thus if i < wdays.Length after the loop, it must be the case that wday == wdays[i].

```csharp
static int WeekDayNo(String wday) {
    int i=0;
    while (i < wdays.Length && wday != wdays[i]) {
        // if i >= wdays.Length or wday == wdays[i]
        if (i < wdays.Length) return i++;
        else return -1;
    }
    static readonly String[] wdays = {
    "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" };
}
```

## Example 126 Searching for a Substring

The call Substring(q,t) returns true if q appears as a substring in t. The outer loop considers all points in t where q could, and the inner loop compares the characters at points to q.

```csharp
static bool Substring(String query, String target) {
    for (int j=0, n=target.Length-query.Length; j<=n; j++) {
        int k=0, m=query.Length;
        while (k<m && target[j+k] == query[k]) {
            // Now if k==m (and target[j..j+m-1] == query[0..m-1])
            k++;
        }
    }
    return false;
}
```

## Example 127 Infinite Loop Because of Misplaced Semicolon

The misplaced semicolon (;) causes the loop to go forever.

```csharp
int i=0;
while (i++)
i++;
```

## Example 128 Using do-while

The do-while statement is used here:

```csharp
int sum = 0;
do {
    sum++;
} while (sum < 5);
```

## 13.7 Returns, Exits, and Jumps

### 13.7.1 The return Statement

The simplest form of return statement, without an argument, is:

```csharp
return;
```

The return statement returns control to the caller. If the method has a return type, the return statement must return a value of that type. If the method is void, the return statement can have no argument.

```csharp
public void Print(String s) {
    Console.WriteLine(s);
    return;
}
```

The return statement returns control to the caller. If the method has a return type, the return statement must return a value of that type. If the method is void, the return statement can have no argument.

```csharp
public int Add(int a, int b) {
    return a + b;
}
```

Alternatively, the return statement can be used to exit a method early:

```csharp
public void Print(String s) {
    if (s == null)
        return; // exit the method early
    Console.WriteLine("String is " + s);
}
```

### 13.7.2 The break Statement

A break statement is legal only inside a switch or loop; it has the form:

```csharp
break;
```

The break statement terminates the innermost loop and continues execution after the loop.

```csharp
for (int i=0; i<10; i++) {
    if (i == 5)
        break;
}
```

### 13.7.3 The continue Statement

A continue statement is legal only inside a loop; it has the form:

```csharp
continue;
```

The continue statement terminates the current iteration of the loop and continues execution at the next iteration of the loop.

```csharp
for (int i=0; i<10; i++) {
    if (i == 5)
        continue;
    Console.WriteLine(i);
}
```
