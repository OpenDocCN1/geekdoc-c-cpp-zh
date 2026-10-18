tion is the same as if the member variable were labeled private. However, in the definition of a member function of a derived class, the variable can be accessed by name. Similarly, if you use the qualifier protected before a member function of a class, then for any class or function other than a derived class (or a derived class of a derived class, etc.), that is the same as if the member function were labeled private. However, in the definition of a member function of a derived class the protected function can be used.
Inherited protected members are inherited in the derived class as if they were marked protected in the derived class. In other words, if a member is marked as protected in a base class, then it can be accessed by name in the definitions of all descendant classes, not just in those classes directly derived from the base class.

# SELF-TEST EXERCISES

+   1. Is the following program legal (assuming appropriate #include and using directives are added)?

```
void showEmployeeData(const Employee object);

int main()
{
    HourlyEmployee joe("Mighty Joe",
        "123-45-6789", 20.50, 40);
    SalariedEmployee boss("Mr. Big Shot",
        "987-65-4321", 10500.50);
    showEmployeeData(joe);
    showEmployeeData(boss);
    return 0;
}
void showEmployeeData(const Employee object)
{
    cout << "Name: " << object.getName() << endl;
    cout << "Social Security Number: "
        << object.getSSN() << endl;
}
```

+   2. Give a definition for a class SmartBut that is a derived class of the base class Smart, which we reproduce for you here. Do not bother with #include directives or namespace details.