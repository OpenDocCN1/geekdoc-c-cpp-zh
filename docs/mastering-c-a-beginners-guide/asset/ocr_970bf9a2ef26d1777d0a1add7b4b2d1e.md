As you can see from the above program, the variable “age” is a local variable that belongs to the function StudentAge(). If you try and use the variable age outside StudentAge() function, the compiler will give away an error:

```
// C# program to demonstrate the error
// due to using the local variable
// outside its scope
using System;
class StudentDetails {
    // Method
    public void StudentAge()
    {
        // local variable age
        int age = 0;
        age = age + 10;
    }
    // Main Method
    public static void Main(String[] args)
    {
        // using local variable age outside
        it's scope
        Console.WriteLine("Student age is
: " + age);
    }
}
```

+   - **Error:** The name “age” does not exist in the current context.

# Instance Variables or Non-Static Variables

Instance variables or non-static variables are the ones announced in a class yet kept outside any method,