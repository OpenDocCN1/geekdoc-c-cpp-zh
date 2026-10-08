As you can see, this is not nearly as simple. However, by utilizing dynamic types, the code becomes that shown in Listing 21.11.

```
**LISTING 21.11**  *Invoking a Method Dynamically*

```
dynamic calculator = GetCalculator();
int sum = calculator.Multiply(6, 7);
```
```

If the Calculator object were defined in a dynamic language such as IronPython, the same code shown in Listing 21.11 could still be used. The only differences would be in the implementation of the GetCalculator method, which would need to create an instance of the IronPython runtime and load the appropriate file, as shown in Listing 21.12.

```
**LISTING 21.12**  *Getting a Dynamic Object from IronPython*

```
dynamic GetCalculator()
{
    ScriptRuntime pythonRuntime = Python.CreateRuntime();
    return pythonRuntime.UseFile("calculator.py");
}
```
```

# ## Summary

Including the Dynamic Language Runtime (DLR) greatly expands the number of languages the .NET Framework can support. It also enables statically typed languages such C# to easily access objects defined in a dynamic language. Using dynamic types allows you to access dynamic objects using code syntax that is essentially the same as you would use if the object were statically defined.

In this hour, you learned the basics of using dynamic types, including how to use ExpandoObject and create your own custom dynamic objects by deriving from DynamicObject. After exploring the basic architecture of the DLR, you then learned how to use dynamic types when working with COM APIs, such as the Office COM API, and objects defined in other languages, such as IronPython.

# ## Q&A

+   * **Q.** *What is a dynamic type?*
* **A.** A dynamic type is one whose operations bypass the compile-time type checking and instead are resolved at runtime.