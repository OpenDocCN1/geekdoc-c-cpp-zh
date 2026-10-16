```
cout << "\t\tWelcome to Blackjack!\n\n";

int numPlayers = 0;
while (numPlayers < 1 || numPlayers > 7)
{
    cout << "How many players? (1 - 7): ";
    cin >> numPlayers;
}

vector<string> names;
string name;
for (int i = 0; i < numPlayers; ++i)
{
    cout << "Enter player name: ";
    cin >> name;
    names.push_back(name);
}
cout << endl;

//the game loop
Game aGame(names);
char again = 'y';
while (again != 'n' && again != 'N')
{
    aGame.Play();
    cout << "\nDo you want to play again? (Y/N): ";
    cin >> again;
}

    return 0;
}
```

The main() function gets the names of all the players and puts them into a vector of string objects, and then instantiates a Game object, passing a reference to the vector. The main() function keeps calling the Game object’s Play() member function until the players indicate that they don’t want to play anymore.

# Overloading the operator<<( ) Function

The following function definition overloads the << operator so I can send a Card object to the standard output.