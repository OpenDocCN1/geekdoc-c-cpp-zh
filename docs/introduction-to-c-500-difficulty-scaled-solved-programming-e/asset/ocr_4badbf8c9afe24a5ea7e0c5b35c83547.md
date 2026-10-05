# 19 • More about Classes 635

```
int main() {
    Publisher pub("Pub");
    pub.set_info("N1", "I1", "A1"); /* set info() should create a
Book object, store its arguments in the respective private members, and
store that object in v book.*/
    pub.set_info("N2", "I2", "A2");
    pub.find("I2"); /* find() should take parameter the isbn of a
book, check if it is contained in the v book, and if yes, it should
dis the name of the publishing team and the book details. For
example, this code should display Pub N2 I2 A2. */
    return 0;
}
```

**U.19.3** Define the class Team and the nested class Player. The Team should contain the add() function, which takes as an argument a Player object and stores it in a vector member (e.g., v_pl). Also, it should contain the show() function, which takes an integer argument (e.g., age) and displays the name of the team, as well as the details of the players who are older the age argument, if any. Finally, it should contain an appropriate constructor. The Player should contain up to three functions. Write a program that implements the code as described in the comments to test the
operation of the classes.

```
class Team {
public:
    class Player {
        private:
            string name; // Name of the player.
            int age; // Age of the player.
        ...
    };
private:
    string name; // Name of the team.
    vector<Player> v_pl;
};
int main() {
    Team team("T");
    /* Create some Player objects and call the add() to store them in
v pl. Then, the program should prompt the user to enter an integer
value that corresponds to the age and pass it as an argument to call
show(). The show() should display the name of the team and the details
of the players who are older, if any. */
    return 0;
}
```

**U.19.4** Define the class Student and the nested class Course. The Course class should contain up to three functions (the constructor should be defined outside the class). Add the appropriate functions to the classes to make the following program work.