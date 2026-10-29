The following class definition corresponds to Figure 13.5:

```
// class declaration section
class NameTele
{
    private:
        string name;
        string phoneNum;

    // class implementation section
    public:
        NameTele(string nn, string phone)  // constructor
        {
            name = nn;
            phoneNum = phone;
        }
        // inline method definitions
        string getName(){return name;}
        string getPhone(){return phoneNum;}
};
```

This class permits constructing objects consisting of name and phoneNum instance variables by using a constructor and accessor methods for setting and retrieving these variables. Program 13.2 instantiates four objects of this class and stores them in a linked list. After it's created, the complete list is displayed.