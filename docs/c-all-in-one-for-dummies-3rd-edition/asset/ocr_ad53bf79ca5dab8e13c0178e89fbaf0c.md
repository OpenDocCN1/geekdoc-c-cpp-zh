Finally, remember that the operator function takes two parameters. You can see their order when you look at the order of cout << myoven. The first is the stream; the second is your class. Thus, when you put this all together, you get the function header we just described, that is

```
```cpp
ostream &operator <<(ostream &out, MicrowaveOven &oven)
```
```

Now, what do you do with this function that you wrote? You just write to the stream passed into it! What do you write? Whatever you want! It's true: Because you designed the class that the function takes as a parameter, you decide how the output looks when you write the object to a stream. So pretend that this is your MicrowaveOven class:

```
```cpp
class MicrowaveOven
{
public:
    int HighVoltageRadiation;
    int RadioactiveFoodCount;
    int LeakLevel;
    string OvenName;
};
```
```

Then your insertion function may look like this:

```
```cpp
ostream &operator <<(ostream &out, MicrowaveOven &oven)
{
    out << "High Voltage Radiation: ";
    out << oven.HighVoltageRadiation << endl;
    out << "Radioactive Food Count: ";
    out << oven.RadioactiveFoodCount << endl;
    out << "Leak Level: ";
    out << oven.LeakLevel << endl;
    out << "Oven Name: ";
    out << oven.OvenName << endl;
    return out;
}
```
```

Now for some points about the preceding code:

+   - We took complete liberty with how we wanted the object to look on the stream. For each member variable, we wrote a description, a colon, a space, and then a value. We then put an endl. Would you like the output to look different? Then go for it! It's your choice how you want the output to look.
+   - We returned the same output stream that came in as the first parameter. This is important!
+   - When we wrote to the stream, we wrote to out, not to cout. If we messed up and wrote to cout, this function would not work properly when used with a file. If we tried myfile << myoven, the information would just go to cout, not into the file. Oops!

![](bbox=[0.08, 0.72, 0.21, 0.86])