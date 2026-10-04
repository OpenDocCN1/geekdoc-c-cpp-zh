# Completing the Basics

```
// check for a leading sign
if (str.at(0) == '-' || str.at(0) == '+')
{
    sign = true;
    start = 1; // start checking for digits after the sign
}

// check that there is at least one character after the sign
if (sign && str.length() == 1) valid = false;

// now check the string, which you know
// has at least one non-digit character
i = start;
while(valid && i < int(str.length()))
{
    if (!isdigit(str.at(i))) valid = false; // found a
    i++; // move to next character
}

return valid;
int getInt()
{
    bool isValidInt(string); // function declaration (prototype)
    bool notant = true;
    string value;

while (notant)
{
    try
    {
        cin >> value; // accept a string input
        if (!isValidInt(value)) throw value;
    } catch (string e)
    {
        cout << "Invalid integer - Please reenter: *";
        continue; // send control to the while statement
    }
    notant = false;
}
return atoi(value.c_str()); // convert to an integer
}
```

The first step in creating a library is to encapsulate all the specialized functions and classes into one or more namespaces and store the complete code (with or without a namespace) into one or more files. For example, you can create one namespace, dataChecks, and save it in the file named dataChecks.cpp. Note that the namespace filename need not be the same as the namespace used in the code.
nThe syntax for creating a namespace is the following:

```
namespace name
{
    // functions and/or classes in here
} // end of namespace
```