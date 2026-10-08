If **buffer** is **bad**() or the source has a problem, we give up; otherwise, we clear **buffer** and try again. We need to clear **buffer** because we get into that “replenish loop” only if a read failed, typically because we hit **eof**() for **buffer**; that is, there were no more characters in **buffer** for us to read. Dealing with stream state is always messy and it is often the source of subtle errors that require tedious debugging. Fortunately the rest of the replenish loop is pretty straightforward:

```
string line;
getline(source, line);              // get a line from source

// do character replacement as needed:
for (char& ch : line)
    if (is_whitespace(ch))
        ch = ' ';                   // to space
    else if (!sensitive)
        ch = tolower(ch);           // to lower case

buffer.str(line);                   // put string into stream
```

We read a line into **line**. Then we look at each character of that line to see if we need to change it. The **is_whitespace**() function is a member of **Punct_stream**, which we’ll define later. The **tolower**() function is a standard library function doing the obvious, such as turning **A** into **a** (see §11.6).

Once we have a properly processed **line**, we need to get it into our **istringstream**. That’s what **buffer.str(line)** does; it can be read as “Set the **istringstream** buffer’s **string** to **line**.”

Note that we “forgot” to test the state of **source** after reading from it using **getline**(). We don’t need to because we will eventually reach the **!****source.good**() test at the top of the loop.

As ever, we return a reference to the stream itself, ***this***, as the result of **>>**; see §17.10.

Testing for whitespace is easy; we just compare a character to each character of the string that holds our whitespace set:

```
bool Punct_stream::is_whitespace(char c)
{
    for (char w : white)
        if (c==w) return true;
    return false;
}
```