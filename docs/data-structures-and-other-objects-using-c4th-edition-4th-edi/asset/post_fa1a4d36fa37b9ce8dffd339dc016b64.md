
## Self-Test Exercises for End of Section 14.2

- 12. Write code to declare a vector of organisms. Put 10 new organisms in the vector, with an initial size of 16 ounces and a growth rate of 1 ounce per week. Grab five random organisms, and alter their growth rates to 2 ounces per week. Finally, calculate the total of all the organisms' growth rates, and print the result.

- 13. In the previous exercise, you started with 10 organisms growing at 1 ounce per week. Five random organisms had their growth rates changed to 2 ounces per week, so you might think that the total of all the organisms' rates would be 5*1 + 5*2, which is 15. But when we ran the program, the total was only 14. Why?

- 14. Design and implement a new class derived from the animal class. The new class, called carnivore, has one new member function with the prototype shown here:

```
void carnivore::chase(animal* prey, double chance);
```

When chase(prey, chance) is activated for some carnivore, the carnivore chases the prey. The probability of actually catching the prey is given by the parameter chance (which should lie between 0 and 1—for example 0.75 for a 75% chance). If the prey actually caught, then this will also activate the carnivore's eat member function and (sadly) activate the prey's death member function.

Note: You can use the rand function (from <cstdlib>) to determine whether the animal is caught, as shown here:

```
if (rand() / double(RAND_MAX) < chance)
{
    // Code for catching and eating the prey
}
```

## 14.3 VIRTUAL MEMBER FUNCTIONS AND A GAME CLASS

This section demonstrates virtual member functions, which are a new kind of member function that allows certain aspects of activating a function to be delayed until a program is actually running.

### Introduction to the game Class

To make the explanation of virtual functions concrete, we'll present an example of a class called game, which will make it easier for us to write programs that play various two-player games such as chess, checkers, or Othello. The games we have in mind will pit a human player against the computer, with the computer making moves that are, hopefully, intelligent.

The key to the game class is the realization that many aspects of these different games can be handled in a uniform way. For example, each game needs a general procedure for going back and forth between the human player and the computer, and each game needs a sensible procedure for selecting the computer's move from among the alternatives. So our proposal is to have a game class that provides all these common operations and will serve as a base class for many derived classes that play various two-player games.

The game class provides a framework for other games to be implemented. For example, a programmer who is writing a chess-playing program can implement a derived chess class that uses the game as a base. Another programmer, writing a program to play Othello, can implement a derived othello class that also uses the game as its base.

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_740_0.png)

The definition of our proposed game class is given in Figure 14.12.

There's a lot of information in the game class definition and it uses several new techniques. We'll briefly explain each part of the definition, and then we'll come back to concentrate on the parts of the definition that must be understood in order to write a derived class such as chess, or Othello, or—as we'll actually do in an example—a derived class to play a game called Connect Four.

### FIGURE 14.12 Definition for the game Class

```
class game
{
public:
// ENUM TYPE
enum { HUMAN, NEUTRAL, COMPUTER }; // Possible game outcomes

// CONSTRUCTOR and DESTRUCTOR
game() { move_number = 0; }
virtual ~game() { }

// PUBLIC MEMBER FUNCTIONS
// The play function should not be overridden. It plays one game, with the human player
// moving first and the computer second. The computer uses an alpha-beta look ahead
// algorithm to select its moves. The return value is the winner of the game (or
// NEUTRAL for a tie).
who play();
```

### (FIGURE 14.12 continued)

```
protected:
// OPTIONAL VIRTUAL FUNCTIONS (overriding these is optional)
virtual void display_message(const std::string& message) const;
virtual std::string get_user_move() const;
virtual who last_mover() const;
virtual int moves_completed() const;
virtual who next_mover() const;
virtual who opposite(who player) const;
virtual who winning() const;

// VIRTUAL FUNCTIONS THAT MUST BE OVERRIDDEN:
// The overriding function should call the original when it finishes.
// Have the next player make a specified move:
virtual void make_move(const std::string& move) { ++move_number; }

// Restart the game from the beginning:
virtual void restart() { move_number = 0; }

// PURE VIRTUAL FUNCTIONS (these must be provided for each derived class)
// Return a pointer to a copy of myself:
virtual game* clone() const = 0;

// Compute all the moves that the next player can make:
virtual void compute_moves(std::queue<std::string>& moves) const = 0;

// Display the status of the current game:
virtual void display_status() const = 0;

// Evaluate a board position (positive values are good for the player who just moved):
virtual int evaluate() const = 0;

// Return true if the current game is finished:
virtual bool is_game_over() const = 0;

// Return true if the given move is legal for the next player:
virtual bool is_legal(const std::string& move) const = 0;

private:
int move_number; // Number of moves made so far
// Other private items could go here, too.
};
```

### The who type.

The class starts with this definition:

```
enum who { HUMAN, NEUTRAL, COMPUTER }; // Possible game outcomes
```

This definition defines an `enum` type, which you might not have used before. An enum type defines a simple new data type along with values that variables of that type can be assigned. In our example, the new enum type is called `who`, and a variable of type `who` can be assigned one of the three constants called `HUMAN`, `NEUTRAL`, and `COMPUTER`. We'll use variables of this type to keep track of who won a game (using `NEUTRAL` for a tie), or whose turn it is to move.

### The constructor.

The game class has a simple constructor that assigns the value zero to its one private member variable (`move_number`). This variable keeps track of how many moves have been made while a game is being played.

### The public play function.

The game class has one public member function:

```
who play ();
```

This function is activated to cause one game to be played. For example, later we will write a class called `connect4`, which is derived from the `game` class and plays a game called Connect Four. A simple `main` function that plays a Connect Four game looks like this:

```
int main ()
{
    connect4 instance;
    connect4::who winner;
    winner = instance.play ();
    switch (winner)
    {
        case connect4::HUMAN: cout << "You win" << endl; break;
        case connect4::COMPUTER: cout << "I win" << endl; break;
        case connect4::NEUTRAL: cout << "A draw" << endl; break;
    }
    return EXIT_SUCCESS;
}
```

This plays one game of Connect Four.

The game is interactive, letting the user type game moves at the keyboard (or, as we will see, the input can come in other ways). A member function of the `game` class directs the computer's moves, searching through all possible moves, looking at responses that the human might make to those moves, and looking at possible responses to the human's responses, and so on.

You are probably wondering about the details of directing the computer's moves. We will discuss that at the end of this section, but for now, let's assume that some wise and generous programmer has given us the complete game class, which we are going to use to implement games such as Connect Four. The wonderful feature of the game class is that we don't need to know the details of how play works in order to write our derived class. We can just trust that our wise and generous programmer wrote the play function correctly. This is one of the big benefits of a well-written base class:

> **The Benefit of a Well-Written Base Class**
> 
> With a well-written base class in hand, a programmer can write derived classes without worrying about how the base class accomplishes its work.

So, we're planning to write a class that is derived from the game class. Among other things, our derived class will inherit the powerful play function. We have no immediate need to understand the details of the play function, but we do need to know more about the next part of the game class definition, which provides a series of protected, virtual functions.

### Protected Members

The next part of the game class definition begins like this:

```
protected:
// OPTIONAL VIRTUAL FUNCTIONS (overriding these is optional)
virtual void display_message(const std::string& message) const;
```

The keyword protected indicates that the items that follow will be a new kind of member, somewhere between public and private. In particular, a protected member can be used (and overridden) by a derived class—but apart from within a derived class, any protected member is private. It cannot be used elsewhere.

### Virtual Member Functions

The first protected member function in the game class is display_message. The game class implements this function is a simple way by printing the message (which is an argument) to the standard output (cout). This works fine, and whenever the play function needs to print a message, it does so by activating display_message. In fact, the beginning of our play function looks like this:

```
game::who game::play()
{
    display_message("Welcome!");
    ...
```
