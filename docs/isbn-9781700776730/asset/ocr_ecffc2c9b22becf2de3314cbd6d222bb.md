# Time Class main() Function

```
int main() {
    Time appt;

    appt.month = 9;
appt.day = 23;
appt.year = 2012;
appt.hour = 8;
appt.min = 30;
appt.sec = 0;

    cout << "Appointment = ";
    appt.display();
}
```

The main() program uses the Time class as much as it would it any other data type.

+   * It declares appt as an object of type Time. The class Time is a template that describes the format of the class members. You must create an object such as appt of the class type in order to use the class.
* It assigns values to appt's data members, initializing a date and time.

Note that we use the dot notation to refer to a class object's public data members just as you refer to members of a struct variable. When such a member is a function, C++ calls the function that typically performs some action upon the class object's data.

# Additional Time Objects

Note that a program might have other Time objects declared as:

```
Time today;
Time yesterday;
Time tomorrow;
```