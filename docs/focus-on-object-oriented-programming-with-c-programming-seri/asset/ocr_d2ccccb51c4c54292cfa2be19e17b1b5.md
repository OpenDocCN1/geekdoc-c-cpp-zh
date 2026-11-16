```
int main() {
    Time2 appt;
    int m, d, y, h, mn, s;
    appt.setTime(7, 23, 2012, 8, 30, 0);
    cout << "Appointment = ";
    appt.display();
    appt.getTime(m, d, y, h, mn, s);
    appt.setTime(m, d, y, ++h, mn, s);
    cout << "Appointment = ";
    appt.display();
}
```

# Time2 Class Additions

The new Time2 class has 3 additions:

+   The private access specifier makes the int data members private to the class. Because of this change, only the class member functions may refer directly to these data members.

> Rule: A classes private data members are available only to members of that class. Private members are invisible outside the class.

Note: By default, members of a class are private. Therefore, the access specifier private: is not needed. For clarity, however, it's a good idea to mark private members with an explicit private access specifier.

+   The two other additions to Time2 are the setTime() and getTime() member functions:

setTime() is used to assign values to the appt class object

getTime() copies appt's data member values to local variables which are passed back to getTime() with the hours incremented.

Along with display() the three member functions limit access to the class's private parts. The only legitimate way to use Time2's private data members is to call one of the class's public member functions. Therefore, as a direct result of encapsulating data and functions in a class, if the data representation changes, only the class's member functions need to be rewritten.