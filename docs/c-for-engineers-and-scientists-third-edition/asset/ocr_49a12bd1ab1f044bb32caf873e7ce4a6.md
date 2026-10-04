# Chapter 10 579

A Case Study: Constructing a Room Object

```
void RoomType::setRoomValues(double l, double w) // this is a mutator
{
    length = l;
    width = w;
}

void RoomType::calculateRoomArea() // this performs a calculation
{
    cout << (length * width);
}
```

```
int main()
{
    RoomType roomOne(12.5, 18.2); // declare a variable of type RoomType
    cout << "The values for this room are:\n";
    roomOne.showRoomValues(); // use a class method on this object
    cout << "\nThe floor area of this room is: \";
    roomOne.calculateRoomArea(); // use another method on this object

    roomOne.setRoomValues(5.5, 10.3); // call the mutator

    cout << "\nThe values for this room have been changed to:\n";
    roomOne.showRoomValues();
    cout << "\nThe floor area of this room is: \";
    roomOne.calculateRoomArea();

    cout << endl;
}
```

The shaded portion of Program 10.4 contains the class construction sections. To see how this class is used, concentrate on the unshaded section containing the main() function. This function creates a room object with a length of 12.5 and a width of 18.2. These room dimensions are displayed using the showRoomValues() function, and the area is calculated and displayed using the calculateRoomArea() function. The room's dimensions are reset and displayed, and the room's area is recalculated. Program 10.4 produces the following output:

Created a new object using the default constructor.

The values for this room are:
length = 12.5
width = 18.2

The floor area of this room is: 227.5

![](bbox=[0.843, 0.923, 0.881, 0.946])