Note that there is no upper limit on the amount of characters making up a string, because it can use varying amounts of memory.

The Boolean type bool is one of the most commonly used variable types in C#, and indeed similar types are equally prolific in code in other languages. Having a variable that can be either true or false has important ramifications when it comes to the flow of logic in an application. As a simple example, consider how many questions can be answered with true or false (or yes and no). Performing comparisons between variable values or validating input are just two of the programmatic uses of Boolean variables that you will examine very soon.

Now that you've seen these types, consider a short example that declares and uses them. In the following Try It Out you use some simple code that declares two variables, assigns them values, and then outputs these values.

# TRY IT OUT Using Simple Type Variables: Ch03Ex01\Program.cs

+   1. Create a new console application called Ch03Ex01 and save it in the directory C:\BegVCSharp\Chapter03.
+   2. Add the following code to Program.cs:
+   3. Execute the code. The result is shown in Figure 3-1.

```
static void Main(string[] args)
{
    int myInteger;
    string myString;
    myInteger = 17;
    myString = "myInteger\" is";
    Console.WriteLine($"{myString} {myInteger}");
    Console.ReadKey();
}
```

![](bbox=[0.18, 0.79, 0.75, 0.88])

# How It Works

The added code performs three tasks:

+   - It declares two variables.
+   - It assigns values to those two variables.
+   - It outputs the values of the two variables to the console.

Variable declaration occurs in the following code:

```
int myInteger;
string myString;
```