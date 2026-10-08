# Example

//declaration section
class FormattedDate
{
public:

```
    FormattedDate();
    void setState(string, string, string, string);
    string formattedDate();
private:
    string month;
    string day;
    string year;
};
```

//implementation section
FormattedDate::FormattedDate()
{

```
    //initializes the private variables
    month = "0";
    day = "0";
    year = "0";
} //end of default constructor
```

```
void FormattedDate::setState(string m, string d, string y)
{
    //assigns program values to the private variables
    month = m;
    day = d;
    year = y;
} //end of setState method
```

```
string FormattedDate::getFormatted()
{
    //formats and returns values stored in the private
    return month + "/" + day + "/" + year;
} //end of getFormatted method
```

Figure F-1 How to define a class

As Figure F-1 shows, a class can contain both public and private members. You record the public members below the keyword public in the class statement. The private members are recorded below the keyword private. When you use a class to instantiate (create) an object in a program, only the public members of the class are exposed (made available) to the program; the private members are hidden. In most cases, you will want to expose the member methods and hide the data members. Therefore, in most class definitions, you will list the method prototypes below the