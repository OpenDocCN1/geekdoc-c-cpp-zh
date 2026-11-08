```
```cpp
string getFirstName() const;
//Function to return the first name.
//Postcondition: The value of firstName is returned.

string getLastName() const;
//Function to return the last name.
//Postcondition: The value of lastName is returned.

personType(string first = "", string last = "");
//Constructor
//Sets firstName and lastName according to the parameters.
//The default values of the parameters are null strings.
//Postcondition: firstName = first; lastName = last;

private:
    string firstName;  //variable to store the first name
    string lastName;   //variable to store the last name
};
```
```

Figure 10-11 shows the UML class diagram of the class personType.

![](bbox=[0.342, 0.463, 0.801, 0.63])

**FIGURE 10-11** UML class diagram of the class *personType*

We now give the definitions of the member functions of the class personType.

```
```cpp
void personType::print() const
{
    cout << firstName << " " << lastName;
}

void personType::setName(string first, string last)
{
    firstName = first;
    lastName = last;
}
```
```