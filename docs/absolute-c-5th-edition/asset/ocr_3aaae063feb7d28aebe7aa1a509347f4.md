# Display 16.7 Demonstration Program for Template Class PFArray (part 2 of 2)

```
for (index = 0; index < 3; index++)
{
    cin >> nextWord;
    b.addElement(nextWord);
}
```

```
cout << "You wrote the following:\n"
count = b.getNumberUsed();
for (index = 0; index < count; index++)
    cout << b[index] << " ";
cout << endl;
cout << "I hope you really mean it.\n";
```

Sample Dialogue

Enter up to 10 nonnegative integers.
Place a negative number at the end.

+   1 2 3 4 5 -1

You entered the following:

+   1 2 3 4 5

Enter three words:

> I love you

You wrote the following:
I love you
I hope you really mean it

> ### Friend Functions

Friend functions are used with template classes in the same way that they are used with ordinary classes. The only difference is that you must include a type parameter where appropriate.

# ## Self-Test Exercise

+   12. What do you have to do to make the following function friend of the template class PFArray in Display 16.5?

```
void showData(PFArray<T> Object);
// Displays the data in theObject to the screen.
// Assumes that << is defined for values of type T.
```