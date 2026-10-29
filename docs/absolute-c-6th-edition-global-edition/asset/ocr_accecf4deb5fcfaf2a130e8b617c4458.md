37. The output is too long to reproduce here. The pattern is as follows:

```
1 times 10 = 10
1 times 9 = 9
.
.
.
1 times 1 = 1
2 times 10 = 20
2 times 9 = 18
.
.
.
2 times 1 = 2
3 times 10 = 30
.
.
```

38. The variable moreToRead is not set to false until we attempt to read past the last item in the file. This means that we will output an extra newline on the last loop iteration. We can address this by outputting the value read first and then reading the next string (and possibly end of file) at the end of the loop iteration. This also handles the case where the file is empty.

```
string text;
bool moreToRead = inputStream >> text;
while (moreToRead)
{
    cout << text << endl;
    moreToRead = inputStream >> text;
}
```

39. The following code reads the first line and then loops that many times.

```
fstream inputStream;

inputStream.open("player.txt");
int numScores;
inputStream >> numScores;
for (int i = 0; i < numScores; i++)
{
    string name;
    int score;
    inputStream >> name;
    inputStream >> score;
    cout << name << ", " << score << endl;
}
inputStream.close();
```