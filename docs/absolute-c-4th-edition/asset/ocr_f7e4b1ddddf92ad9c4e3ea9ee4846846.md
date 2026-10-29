# Display 14.6 Implementation for the Derived Class SalariedEmployee (part 2 of 2)

```
42      cout << "Salaried Employee. Regular Pay: "
43      cout << salary << endl;
44      cout << "--------------------------------------------------\n";
45    }
46 }//SavitchEmployees
```

# CONSTRUCTORS IN DERIVED CLASSES

A constructor in a base class is not inherited in the derived class, but you can invoke a constructor of the base class within the definition of a derived class constructor, which is all you need or normally want. A constructor for a derived class uses a constructor from the base class in a special way: A constructor for the base class initializes all the data inherited from the base class. Thus, a constructor for a derived class begins with an invocation of a constructor for the base class. The special syntax for invoking the base class constructor is illustrated in the constructor definitions for the class HourlyEmployee given in Display 14.5. In what follows we have reproduced (with minor changes in the line breaks to make it fit the text column) one of the constructor definitions for the class HourlyEmployee taken from that display:

```
HourlyEmployee::HourlyEmployee(string theName,
    string theNumber, double theWageRate, double theHours)
  : Employee(theName, theNumber),
    wageRate(theWageRate), hours(theHours)
{
    //deliberately empty
}
```

The portion after the colon is the initialization section of the constructor definition for the constructor HourlyEmployee::HourlyEmployee. The part Employee(theName, theNumber) is an invocation of the two-argument constructor for the base class Employee. Note that the syntax for invoking the base class constructor is analogous to the syntax used to set member variables: The entry wageRate(theWageRate) sets the value of the member variable wageRate to theWageRate; the entry Employee(theName, theNumber) invokes the base class constructor Employee with the arguments theName and theNumber. Since all the work is done in the initialization section, the body of the constructor definition is empty.

Below we reproduce the other constructor for the class HourlyEmployee from Display 14.5:

```
HourlyEmployee::HourlyEmployee() : Employee(), wageRate(0),
    hours(0)
{
    //deliberately empty
}
```