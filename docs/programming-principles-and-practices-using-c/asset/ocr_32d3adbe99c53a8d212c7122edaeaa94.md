Every **Document** starts out with a single empty line: **Document’s** constructor makes an empty line and pushes it into the list of lines.
Reading and splitting into lines can be done like this:

```
```c++
istream& operator>>(istream& is, Document& d)
{
    for (char ch; is.get(ch); ) {
        d.line.back().push_back(ch);        // add the character
        if (ch==’\n')
            d.line.push_back(Line{});       // add another line
    }
    if (d.line.back().size()) d.line.push_back(Line{}); // add final empty line
    return is;
}
```
```

Both **vector** and **list** have a member function **back()** that returns a reference to the last element. To use it, you have to be sure that there really is a last element for **back()** to refer to – don’t use it on an empty container. That’s why we defined a **Document** to end with an empty **Line**. Note that we store every character from input, even the newline characters (\"\"\"\n\"\"\"). Storing those newline characters greatly simplifies output, but you have to be careful how you define a character count (just counting characters will give a number that includes space and newline characters).

# ### 20.6.2 Iteration

If the document was just a **vector\u003cchar\u003e** it would be simple to iterate over it. How do we iterate over a list of lines? Obviously, we can iterate over the list using **list\u003cLine\u003e::iterator**. However, what if we wanted to visit the characters one after another without any fuss about line breaks? We could provide an iterator specifically designed for our **Document:**

```
```c++
class Text_iterator {  // keep track of line and character position within a line
    list<Line>::iterator ln;
    Line::iterator pos;
public:
    // start the iterator at line ll's character position pp:
    Text_iterator(list<Line>::iterator ll, Line::iterator pp)
        :ln(ll), pos(pp) { }

    char& operator*() { return *pos; }
    Text_iterator& operator++();
};
```
```