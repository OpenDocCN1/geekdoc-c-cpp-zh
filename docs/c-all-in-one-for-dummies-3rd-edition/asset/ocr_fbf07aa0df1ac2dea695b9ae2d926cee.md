In addition to the main `EthicalCompetition` class, you might create additional auxiliary classes that the `EthicalCompetition` class will use, but your coworkers will not directly create instances of. One might be a class called `Connection` that handles the tasks of connecting to the competitor’s computer.

Here’s the first problem: The class `Connection` may be something you write, but *another* class somewhere may be called `Connection`, and your coworkers might need to use that class. And here’s the second problem: If you have that `Connection` class, you may not want your coworkers using it. You just want them using the main interface, the `EthicalCompetition` class.

To solve the unique name problem, you have several choices. For one, you can just rename the class something a bit more unique, such as `EthicalCompetitionConnection`. But that’s a bit long. And why go through all that trouble if it’s not even going to be used except internally in the code for `EthicalCompetition`? However, you could shorten the classname and call it something that’s likely to be unique, such as `ECConnection`.

Yet at the same time, if the users of your classes look at the header file and see a whole set of classes, which classes they should be using may not be clear. (Of course, you would write some documentation to clear this up, but you do want the code to be at least somewhat self-explanatory.)

One solution is to use *nested* classes. With a nested class, you write the declaration for the main class, `EthicalCompetition`, and then, inside the class, you write the supporting classes, as in the following:

```
```cpp
class EthicalCompetition
{
private:
    class Connection
    {
    public:
        void Connect();
    };

public:
    void HardWork();
};
```
```

Note that we wrote a class inside a class. We did not provide the code for the functions themselves, so here they are:

```
```cpp
void EthicalCompetition::HardWork()
{
    Connection c;
    c.Connect();
    cout << "Connected" << endl;
}
```
```