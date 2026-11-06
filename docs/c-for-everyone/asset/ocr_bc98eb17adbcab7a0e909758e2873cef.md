A good illustration of the use of sets is a program to check for misspelled words. Assume you have a file containing correctly spelled words (that is, a dictionary), and a second file you wish to check. The program reads a file containing a dictionary of correctly spelled words into a set, then reads words from the second file and tests each in the set, printing the word if it is not found.

```
void spell_check(istream& dictionary, istream& text)
{
    set<string> words;
    string word;

    // First put all words from the dictionary into the set
    while (dictionary >> word)
    {
        words.insert(word);
    }

    // Then read words from text
    while (text >> word)
    {
        if (words.count(word) == 0)
        {
            cout << "Misspelled word " << word << endl;
        }
    }
}
```

![](bbox=[0.113, 0.468, 0.201, 0.554])

# SELF CHECK

+   1. Arrays and lists remember the order in which you added elements; sets do not. Why would you want to use a set instead of an array or list?

+   2. Why are set iterators different from list iterators?

+   3. What is the output of the following code snippet?

```
set<int> s;
for (int i = 1; i <= 4; i++)
{
    s.insert(i * i);
    s.insert(-i);
}
for (set<int>::iterator p = s.begin(); p != s.end(); p++) { cout << *p << " "; }
```

+   4. What is the output of the following code snippet?

```
set<int> s;
for (int i = 0; i < 20; i = i + 2) { s.insert(i); }
for (int i = 0; i < 20; i = i + 2) { s.remove(i); }
for (set<int>::iterator p = s.begin(); p != s.end(); p++) { cout << *p << " "; }
```

+   5. What does the following code do, given two sets<string> named a and b?

```
set<string> c;
for (set<string>::iterator p = a.begin(); p != a.end(); p++) { c.insert(*p); }
for (set<string>::iterator p = b.begin(); p != b.end(); p++)
{
    if (a.count(*p) == 0) { c.remove(*p); }
}
```

**Practice It**  Now you can try these exercises at the end of the chapter: R14.1, R14.2, P14.3.