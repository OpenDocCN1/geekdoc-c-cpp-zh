# Object-Oriented Programming with C++

```
linemap[iLineNum]=line;
line.erase();
```

We also erase the contents of the line string object so that the next line can be loaded
afresh.

Now, we come to the last portion of the code wherein the loop accepts the word to be
searched from the user and returns the results.

After prompting the user, we first clean up the variable in which the word entered by the
user would be stored. The readers are appended to the word variable until user
presses the enter key.

The test breaks the potentially infinite loop is as follows:

```
if(word.empty())
```

It has been inserted in the middle since we don't want the rest of the loop to execute. If
t user enters a blank string, the loop breaks and the program terminates.
If the user does not enter a blank string, we try to find it in the word map.

```
iter=wordmap.find(word);
```

If the word is found in the word map, this iterator points at the element whose member
is the word itself and second element is a vector of locations of the found word. The
size of this vector gives us the number of occurrences of the found word.

```
for(witer=iter->second.begin());
witer!=iter->second.end();witer++)
```

iterates through the vector of locations of the found word. Each element of the vector is a pair
line position and word position. The locations are displayed by enclosing these positions
in brackets and separating them by commas.

Passing the line position to the line vector returns the corresponding line. This is also
disayed in the loop.

```
cout<<. <<linemap[witer->first].c_str()<<endl;
```