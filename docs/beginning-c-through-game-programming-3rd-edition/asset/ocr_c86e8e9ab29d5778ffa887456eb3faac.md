# Using the find() Algorithm

After I display the contents of the vector scores, I get a value from the user to find and store it in the variable score. Then I use the find() algorithm to search the vector for the value:

```
iter = find(scores.begin(), scores.end(), score);
```

The find() STL algorithm searches a specified range of a container’s elements for a value. It returns an iterator that references the first matching element. If no match is found, it returns an iterator to the end of the range. You must pass the starting point as an iterator, the ending point as an iterator, and a value to find. The algorithm searches from the starting iterator up to but not including the ending iterator. In this case, I passed scores.begin() and scores.end() as the first and second arguments to search the entire vector. I passed score as the third argument to search for the value the user entered.

Next I check to see if the value score was found:

```
if (iter != scores.end())
{
    cout << "Score found.\n";
}
else
{
    cout << "Score not found.\n";
}
```

Remember, iter will reference the first occurrence of score in the vector, if the value was found. So, as long as iter is not equal to scores.end(), I know that score was found and I display a message saying so. Otherwise, iter will be equal to scores.end() and I know score was not found.

# Using the random_shuffle() Algorithm

Next I prepare to randomize the scores using the random_shuffle() algorithm. Just as when I generate a single random number, I seed the random number generator before I call random_shuffle(), so the order of the scores might be different each time I run the program.

```
srand(static_cast<unsigned int>(time(0)));
```

Then I reorder the scores in a random way.

```
random_shuffle(scores.begin(), scores.end());
```