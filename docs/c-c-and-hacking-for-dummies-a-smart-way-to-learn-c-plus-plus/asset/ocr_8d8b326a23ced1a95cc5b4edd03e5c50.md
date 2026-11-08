value to each of the variables of the individual player, we will be creating a new record, or a new object that exists within Class Player. Every object will consist of a name, age and income. In order to declare the variables of each Player type, we use the same method as we would declaring any other variable:

```
Player player1;
Player player2;
Player player 3;
```

Once we have created a Class as seen in the first example, we can use it like any other example of data type that we have previously used. However, we want to also be able to limit what the program is able to access and manipulate within these class structures. Some objects or classes must remain the same at all times (private class), where some can be changed (public). For example, the class which contains only name, age and income must remain private, as this is a constant. On the other hand, the variables that we declare for each individual is public, because that information is not constant.

To see this in code, we would write the following:

```
Class Player
{
private:
    string name;
    string age;
    double income;

public:
    Player();
};
```

Executing the above lines of code would prohibit the program from being able to make changes to the private class of name, age and income, but would allow it to make changes to the public class of individual player information. We use “:” after declaring private and public, because they tell the program that everything afterwards is considered that class type.