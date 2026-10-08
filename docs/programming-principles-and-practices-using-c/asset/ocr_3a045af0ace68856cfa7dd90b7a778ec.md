called **buffer**. Now we can use the usual whitespace-separating `>>` to read from **buffer**. The code looks a bit more complicated than this because we simply try reading from the **buffer** and try to fill it only when we find it empty:

```
```cpp
Punct_stream& Punct_stream::operator>>(string& s)
{
  while (! (buffer>>s)) {   // try to read from buffer
    if (buffer.bad() || !source.good()) return *this;
    buffer.clear();

    string line;
    getline(source,line);   // get a line from source

    // do character replacement as needed:
    for (char& ch : line)
      if (is_whitespace(ch))  // to space
        ch = ' ';
      else if (!sensitive)  // to lower case
        ch = tolower(ch);

    buffer.str(line);   // put string into stream
  }
  return *this;
}
```
```

Let’s consider this bit by bit. Consider first the somewhat unusual

```
```cpp
while (! (buffer>>s)) {
```
```

If there are characters in the `istringstream` called **buffer**, the read `buffer>>s` will work, and `s` will receive a “whitespace”-separated word; then there is nothing more to do. That will happen as long as there are characters in **buffer** for us to read. However, when `buffer>>s` fails – that is, if `! (buffer>>s)` – we must replenish **buffer** from `source`. Note that the `buffer>>s` read is in a loop; after we have tried to replenish **buffer**, we need to try another read, so we get

```
```cpp
while (! (buffer>>s)) {   // try to read from buffer
  if (buffer.bad() || !source.good()) return *this;
  buffer.clear();

  // replenish buffer
}
```
```