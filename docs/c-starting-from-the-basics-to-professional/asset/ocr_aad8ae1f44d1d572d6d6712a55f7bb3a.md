```
```cpp
int main()
{
    for (int i {}; i < 7; ++i)
    {
        try
        {
            if (i == 3)
                throw Trouble{};
            else if (i == 5)
                throw MoreTrouble{};
            else if (i == 6)
                throw BigTrouble{};
        }
        catch (const BigTrouble& t)
        {
            std::cout << "BigTrouble object caught: " << t.what() << std::endl;
        }
        catch (const MoreTrouble& t)
        {
            std::cout << "MoreTrouble object caught: " << t.what() << std::endl;
        }
        catch (const Trouble& t)
        {
            std::cout << "Trouble object caught: " << t.what() << std::endl;
        }

        std::cout << "End of the for loop (after the catch blocks) - i is " << i << std::endl;
    }
}
```
```

Here’s the output:

```
```
End of the for loop (after the catch blocks) - i is 0
End of the for loop (after the catch blocks) - i is 1
End of the for loop (after the catch blocks) - i is 2
Trouble object caught: There's a problem
End of the for loop (after the catch blocks) - i is 3
End of the for loop (after the catch blocks) - i is 4
MoreTrouble object caught: There's more trouble...
End of the for loop (after the catch blocks) - i is 5
BigTrouble object caught: Really big trouble...
End of the for loop (after the catch blocks) - i is 6
```
```

Inside the for loop, objects of type Trouble, MoreTrouble, and BigTrouble are thrown as an exception. These objects are constructed at the moment they are thrown, as is often the case with exceptions. The type of object that is thrown depends on the value of the loop variable, i. Each of the catch blocks contains a different message, so the output shows which catch handler is selected when an exception is thrown. In the handlers for the two derived types, the inherited what() function still returns the message. Note that the parameter type for each of the catch blocks is a reference, as in the previous example. One reason for using a reference is to avoid making an unnecessary copy of the exception object. In the next example, you’ll see another, more crucial reason why you should always use a reference parameter in a handler.