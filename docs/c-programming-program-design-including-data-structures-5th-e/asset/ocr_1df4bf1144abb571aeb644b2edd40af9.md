![](bbox=[0.204, 0.107, 0.887, 0.305])

**FIGURE 11-11**  UML class diagram of the class `personType`

We now give the definitions of the member functions of the class `personType`.

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

string personType::getFirstName() const
{
    return firstName;
}

string personType::getLastName() const
{
    return lastName;
}

//constructor
personType::personType(string first, string last)
{
    firstName = first;
    lastName = last;
}
```
```