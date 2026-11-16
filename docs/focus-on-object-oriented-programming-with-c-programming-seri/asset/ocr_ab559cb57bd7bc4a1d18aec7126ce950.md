# ## Substring Function

It is often useful to be able to access substrings of String objects. We'll need to extract and return the substring of a String object starting at a particular index in the buffer and of a specified length.

```
String substr(int, int);
```

# ## Output Function

In order to display the state of any String object, we have to write a print function. This function outputs the literal itself between double quotation marks and outputs the length of the string literal on the same line.

```
void print();
```

It is also useful to overload the operator<<() function to output just the contents of the string pointer itself.

```
friend ostream& operator<<(ostream&, const String&);
```

# ## Class Inheritance

Inheritance is the process by which a derived class is created as the result of extending, or enhancing, an existing class. Stated differently, the derived class is inherited from a parent (or base) class. This capability saves you from having to "reinvent the wheel", because if a new class greatly resembles an existing class, then all of the properties of the existing class can be inherited into the new class, and any new members can then be added.

Inheritance allows you to collect related classes into a hierarchy with the classes at the top serving as abstractions for those below. This implies that a derived class is a specialization of its parent class. In other words, the derived class is a type of base class, but with more detail added. For this reason, the relationship between a derived class and its base class is called an is-a relationship.

We've seen how a String class could be created and then utilize the capabilities of operator function overloading to make the class interface more