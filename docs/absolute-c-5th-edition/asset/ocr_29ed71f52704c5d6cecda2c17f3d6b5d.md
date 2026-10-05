# 500 CHAPTER 11 Separate Compilation and Namespaces

Display 11.9 Hiding the Helping Functions in a Namespace (Implementation File) (part 2 of 3)

```
if (! ( isdigit(c1) && isdigit(c2) || c2 == ':') ))
{
    cout << "Error: illegal input to readHour\n"
    exit(1);
}

if (isdigit(c1) && c2 == ':')
{
    theHour = digitToInt(c1)*10 + digitToInt(c2);
    cin >> c2; //discard '':
    cout << "Error: illegal input to readHour\n"
    exit(1);
}

if (theHour == 24)
    theHour = 0; //Standardize midnight as 0:00;

if (theHour < 0 || theHour > 23)
{
    cout << "Error: illegal input to readHour\n"
    exit(1);
}
}
//unnamed namespace
namespace DTimeSavitch
{
    //Uses istream
istream& operator >>(istream& ins, DigitalTime&theObject)
{
        // Within the compilation unit (in this case
        datetime.cpp), you can use names in the
        unnamed namespace without qualification.
        readHour(theObject.hour);
        readMinute(theObject.minute);
        return ins;
}
ostream& operator <<(ostream& outs, const DigitalTime&theObject)
    //The body of the function definition is the same as in Display 11.2>
```