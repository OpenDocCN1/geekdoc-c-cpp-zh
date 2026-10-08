example from §4.6.3 where we read in “words” and compared them. Those words were whitespace-separated, so if we read

> *As planned, the guests arrived; then,*

We would get the “words”

+   * As
* planned,
* the
* guests
* arrived;
* then,

This is not what we’d find in a dictionary: **planned,** and **arrived;** are not words. They are words plus distracting and irrelevant punctuation characters. For most purposes we must treat punctuation just like whitespace. How might we get rid of such punctuation? We could read characters, remove the punctuation characters — or turn them into whitespace — and then read the “cleaned-up” input again:

```
```
string line;
getline(cin,line);        // read into line
for (char& ch : line)    // replace each punctuation character by a space
    switch(ch) {
        case ';': case '.': case ',': case '?': case '!':
            ch = ' ';
    }

stringstream ss(line);   // make an istream ss reading from line
vector<string> vs;
for (string word; ss>>word; ) // read words without punctuation characters
    vs.push_back(word);
```
```

Using that to read the line, we get the desired

+   * As
* planned
* the
* guests
* arrived
* then