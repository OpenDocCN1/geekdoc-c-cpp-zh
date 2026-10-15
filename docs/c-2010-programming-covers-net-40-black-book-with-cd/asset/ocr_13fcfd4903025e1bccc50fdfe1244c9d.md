```
class EventTestClass
{
    // The value to track
    private int nvalue;
    // Allow a handler for the event
    public delegate Boolean ValueChangedEventHandler(int nvalue);
    // This is the event itself
    public event ValueChangedEventHandler Changed;
    // This method is used to fire the event
    protected virtual Boolean OnChanged(int nv)
    {
        return true;
    }
    public EventTestClass(int nvalue)
    {
        SetValue(nvalue);
    }
    public void SetValue(int nv)
    {
        if (nvalue != nv)
        {
            if (OnChanged(nv))
            nValue = nv;
            // Fire the event
        }
    }
    static void Main(string[] args)
    {
    }
}
```

It can be seen that Listing 34.2 uses the complete spectrum of possible types in the C# system, such as enumerations, interfaces, structures, and classes.

+   4. Save the file as EventTestClass.cs in the D:\Black Books\C# 2010\Chapter 34 folder.
+   5. Open the Visual Studio 2010 command prompt by navigating to the following menu path: Visual Studio Tools→Visual Studio Command Prompt (2010)
+   6. Start→All Programs→Microsoft Visual Studio 2010→Visual Studio Tools→Visual Studio Command Prompt (2010)
+   7. Navigate to the D:\Black Books\C# 2010\Chapter 34 folder location on the Visual Studio command prompt.
+   8. Compile the ObtainClassInformation.cs and EventTestClass.cs files, one by one, by using the following commands:
+   csc obtainClassInformation.cs
+   csc EventTestClass.cs
+   9. Execute the following command to see the output of these files:
+   ObtainClassInformation.exe EventTestClass.exe

You should note that when you compile the ObtainClassInformation.cs and EventTestClass.cs files, the ObtainClassInformation.exe and EventTestClass.exe files are generated in the D:\Black Books\C# 2010\Chapter 34 folder.

Figure 34.1 shows the output of the preceding command: