```
for (count = WIN ; count <= CANCEL ; count++)
{
    result = (game_result)count;
    if (result == omit)
    {
        cout << "The game was cancelled\n";
    }
    else
    {
        cout << "The game was played ";
        if (result == WIN)
            cout << "and we won!";
        if (result == LOSE)
            cout << "and we lost.";
        cout << "\n";
    }
n
```

Result:

| The game was played and we won |
| game was played and we lost |
| game was played |
| game was cancelled |

Notice:

game_result result;
enum game_result omit = CANCEL;
The above two statements are both right. After declaring an enumeration type, we do not need to write the keyword enum before the type name when declaring a variable.

# 2.5.3 Structure

We have learned basic data types and the enumeration type (a collection of integers) so far, in many cases we need to combine different data types together. For example, consider the student number, name, age, and score of one. Although they are of different data types, they are closely related in they belong to one person. In this case, we need to declare a structure type for this group of information. Structure type is a collection of different types of data, and its declaration form is as below: