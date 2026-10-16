

move (found is true) that I want the computer to make (square number move) to block the human from winning on his next move.

Next, I check to see if I need to go on to Step 3 of my AI strategy. If I haven’t found a move yet (found is false), then I look through the list of best moves, in order of desirability, and take the first legal one.

```
//otherwise, moving to the best open square is the move to make
if (!found)
{
    move = 0;
    unsigned int i = 0;

    const int BEST_MOVES[] = {4, 0, 2, 6, 8, 1, 3, 5, 7};
    //pick best open square
    while (!found && i < board.size())
    {
        move = BEST_MOVES[i];
        if (isLegal(move, board))
        {
            found = true;
        }

        ++i;
    }
}
```

At this point in the function, I’ve found the move I want the computer to make—whether that’s a move that gives the computer a win, blocks a winning move for the human, or is simply the best empty square available. So, I have the computer announce the move and return the corresponding square number.

```
cout << "I shall take square number " << move << endl;
return move;
}
```

## Real World

> The Tic-Tac-Toe game considers only the next possible move. Programs that play serious games of strategy, such as chess, look far deeper into the consequences of individual moves and consider many levels of moves and countermoves. In fact, good computer chess programs can consider literally millions of board positions before making a move.

## The announceWinner() Function

This function receives the winner of the game, the computer’s piece, and the human’s piece. The function announces the winner or declares a tie.

```
void announceWinner(char winner, char computer, char human)
{
    if (winner == computer)
    {
        cout << winner << "'s won!\n";
        cout << "As I predicted, human, I am triumphant once more -- proof\n";
        cout << "that computers are superior to humans in all regards.\n";
    }
    else if (winner == human)
    {
        cout << winner << "'s won!\n";
        cout << "No, no! It cannot be! Somehow you tricked me, human.\n";
        cout << "But never again! I, the computer, so swear it!\n";
    }
    else
    {
        cout << "It's a tie.\n";
        cout << "You were most lucky, human, and somehow managed to tie me.\n";
        cout << "Celebrate... for this is the best you will ever achieve.\n";
    }
}
```

## SUMMARY

In this chapter, you should have learned the following concepts:

- A reference is an alias; it’s another name for a variable.
- You create a reference using &—the referencing operator.
- A reference must be initialized when it’s defined.
- A reference can’t be changed to refer to a different variable.
- Whatever you do to a reference is done to the variable to which the reference refers.
- When you assign a reference to a variable, you create a new copy of the referenced value.

Still others opt for `int &ref = var;`. The computer is fine with all three. There are cases to be made for each style; however, the most important thing is to be consistent.

Q: Why can’t I initialize a non-constant reference with a constant value?

A: Because a non-constant reference allows you to change the value to which it refers.

Q: If I initialize a constant reference with a non-constant variable, can I change the value of the variable?

A: Not through the constant reference because when you declare a constant reference, you’re saying that the reference can’t be used to change the value to which it refers (even if that value can be changed by other means).

Q: How does passing a constant reference save overhead?

A: When you pass a large object to a function by value, your program makes a copy of the object. This can be an expensive operation depending on the size of the object. Passing a reference is like only passing access to the large object; it is an inexpensive operation.

Q: Can I make a reference to a reference?

A: Not exactly. You can assign one reference to another reference, but the new reference will simply refer to the value to which the original reference refers.

Q: What happens if I declare a reference without initializing it?

A: Your compiler should complain because it’s illegal.

Q: Why should I avoid changing the value of a variable that I pass through a reference?

A: Because it could lead to confusion. It’s impossible to tell from only a function call whether a variable is being passed to change its value.

Q: Does that mean I should always pass a constant reference?

A: No. You can pass a non-constant reference to a function, but to most game programmers, this signals that you intend to change the argument variable’s value.

Q: If I don’t change the argument variables passed to functions, how should I get new information back to the calling code?

A: Use return values.

Q: Can I pass a literal through a non-constant reference?

A: No. If you try to pass a literal as a non-constant reference, you’ll generate a compile error.

Q: Is it impossible to pass a literal to a parameter that accepts a reference?

A: No, you can pass a literal as a constant reference.

Q: What happens when I return an object from a function?

A: Normally, your program creates a copy of the object and returns that. This can be an expensive operation, depending on the size of the object.

Q: Why return a reference?

A: It can be more efficient because returning a reference doesn’t involve copying an object.

Q: How can I lose the efficiency of returning a reference?

A: By assigning the returned reference to a variable. When you assign a reference to a variable, the computer must make a copy of the object to which the reference refers.

Q: What’s wrong with returning a reference to a local variable?

A: The local variable doesn’t exist once the function ends, which means that you’re returning a reference to a non-existent object, which is illegal.

## Discussion Questions

- 1. What are the advantages and disadvantages of passing an argument by value?
- 2. What are the advantages and disadvantages of passing a reference?
- 3. What are the advantages and disadvantages of passing a constant reference?

4. What are the advantages and disadvantages of returning a reference?

5. Should game AI cheat in order to create a more worthy opponent?

## EXERCISES

1. Improve the Mad Lib game from Chapter 5 by using references to make the program more efficient.

2. What’s wrong with the following program?

```
int main()
{
    int score;
    score = 1000;
    float& rScore = score;
    return 0;
}
```

3. What’s wrong with the following function?

```
int& plusThree(int number)
{
    int threeMore = number + 3;
    return threeMore;
}
```

This page intentionally left blank

## CHAPTER 7

## Pointers: Tic-Tac-Toe 2.0

![](img/34f09be0ed6217c465debc4490197d4f_245_0.png)

Pointers are a powerful part of C++. In some ways, they behave like iterators from the STL. Often, you can use them in place of references. But pointers offer functionality that no other part of the language can. In this chapter, you’ll learn the basic mechanics of pointers and get an idea of what they’re good for. Specifically, you’ll learn to:

- Declare and initialize pointers
- Dereference pointers
- Use constants and pointers
- Pass and return pointers
- Work with pointers and arrays

## Understanding Pointer Basics

Pointers have a reputation for being difficult to understand. In reality, the essence of pointers is quite simple—a pointer is a variable that can contain a memory address. Pointers give you the ability to work directly and efficiently with computer memory. Like iterators from the STL, they’re often used to access the contents of other variables. But before you can put pointers to good use in your game programs, you have to understand the basics of how they work.

## Hint

Computer memory is a lot like a neighborhood, but instead of houses in which people store their stuff, you have memory locations where you can store data. Just like a neighborhood where houses sit side by side, labeled with addresses, chunks of computer memory sit side by side, labeled with addresses. In a neighborhood, you can use a slip of paper with a street address on it to get to a particular house (and to the stuff stored inside it). In a computer, you can use a pointer with a memory address in it to get to a particular memory location (and to the stuff stored inside it).

## Introducing the Pointing Program

The Pointing program demonstrates the mechanics of pointers. The program creates a variable for a score and then creates a pointer to store the address of that variable. The program shows that you can change the value of a variable directly, and the pointer will reflect the change. It also shows that you can change the value of a variable through a pointer. It then demonstrates that you can change a pointer to point to another variable entirely. Finally, the program shows that pointers can work just as easily with objects. Figure 7.1 illustrates the results of the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 7 folder; the filename is pointing.cpp.

![](img/34f09be0ed6217c465debc4490197d4f_246_0.png)

Figure 7.1
The pointer pScore first points to the variable score and then to the variable newScore, while the pointer pStr points to the variable str.

