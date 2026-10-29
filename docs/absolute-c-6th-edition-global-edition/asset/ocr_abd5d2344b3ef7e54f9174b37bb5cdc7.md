# Display 16.7 Demonstration Program for Template Class PFArray (part 2 of 2)

```
39   for (index = 0; index < 3; index++)
40   {
41       cin >> nextWord;
42       b.addElement(nextWord);
43   }
44
45   cout << "You wrote the following:\n";
46   count = b.getNumberUsed();
47   for (index = 0; index < count; index++)
48       cout << b[index] << " ";
49   cout << endl;
50   cout << "I hope you really mean it.\n";
51
52   return 0;
53 }
```

# Sample Dialogue

```
Enter up to 10 nonnegative integers.
Place a negative number at the end.
1 2 3 4 5 -1
You entered the following:
1 2 3 4 5
Enter three words:
I love you
You wrote the following:
I love you
I hope you really mean it
```

# Friend Functions

Friend functions are used with template classes in the same way that they are used with ordinary classes. The only difference is that you must include a type parameter where appropriate.

# Self-Test Exercise

12. What do you have to do to make the following function a friend of the template class PFArray in Display 16.5?

void showData(PFArray<T>& theObject);
//Displays the data in theObject to the screen.
//Assumes that << is defined for values of type T.