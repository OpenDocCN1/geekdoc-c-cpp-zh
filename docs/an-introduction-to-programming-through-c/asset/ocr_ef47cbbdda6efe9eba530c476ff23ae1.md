```
void right(double angle){
    t.right(angle);
}
void left(double angle){
    t.left(angle);
}
// similar forwarding code for other functions allowed on Turtle..
};
```

As you can see, inside mTurtleC we have a Turtle object which you will see on the screen, and a member distance which keeps track of how much the turtle has moved. Clearly, when an mTurtleC is created, we should set distance to 0, which is what the constructor above does. The constructor does not appear to do much with the turtle member t. But you know that the member t is also created, using the default Turtle constructor. Thus a turtle will appears on the screen. The member function forward in mTurtleC causes distance to be updated, and causes the turtle to move as well. Finally, the member function distanceCovered prints distance as expected.

The code for right is simple, we just call the function right on member t, with the same argument. We will have to write such forwarding functions for other functions such as left, hide and so on.

Clearly, this will enable us to write the main program given earlier; we merely have to use mTurtleC in it instead of mTurtle. The solution is fairly satisfactory, the main drawback is the need to write the forwarding functions.

# 23.1.2 Implementation using Inheritance

Using inheritance, we can define a metered turtle more compactly, as follows. We will call this class mTurtleI.

```
class mTurtleI : public Turtle{ // solution with inheritance
    float distance;
public:
    mTurtleI(){
        distance = 0;
    }
    void forward(float d){
        distance += abs(d);
        Turtle::forward(d);
    }
    float distanceCovered(){
        return distance;
    }
};
```

We will shortly explain what each line in this does. For now we merely note that this will essentially do what the code in Section 23.1.1 did. With this, we will be able to run the