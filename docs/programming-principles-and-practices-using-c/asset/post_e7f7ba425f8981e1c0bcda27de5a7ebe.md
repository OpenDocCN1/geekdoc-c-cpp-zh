
Here, we use `auto` because it is not all that easy to name the element type of the container `cont`. We use `const` because we are not writing to the container elements, and we use `&` (for reference) in case the elements are so large that copying them would be costly.

## 20.6 An example: a simple text editor

The essential feature of a list is that you can add and remove elements without moving other elements of the list. Let’s try a simple example that illustrates that. Consider how to represent the characters of a text document in a simple text editor. The representation should make operations on the document simple and reasonably efficient.

Which operations? Let’s assume that a document will fit in your computer’s main memory. That way, we can choose any representation that suits us and simply convert it to a stream of bytes when we want to store it in a file. Similarly, we can read a stream of bytes from a file and convert those to our in-memory representation. That decided, we can concentrate on choosing a convenient in-memory representation. Basically, there are five things that our representation must support well:

- Constructing it from a stream of bytes from input
- Inserting one or more characters
- Deleting one or more characters
- Searching for a string
- Generating a stream of bytes for output to a file or a screen

The simplest representation would be a `vector<char>`. However, to add or delete a character we would have to move every following character in the document. Consider:

> This is he start of a very long document.
> There are lots of . . .

We could add the **t** needed to get

> This is the start of a very long document.
> There are lots of . . .

However, if those characters were stored in a single `vector<char>`, we’d have to move every character from **h** onward one position to the right. That could be a lot of copying. In fact for a 70,000-character-long document (such as this chapter, counting spaces), we would, on average, have to move 35,000 characters to insert or delete a character. The resulting real-time delay is likely to be noticeable and annoying to users. Consequently, we “break down” our representation into “chunks” so that we can change part of the document without moving a lot of characters around. We represent a document as a list of “lines,” `list<Line>`, where a `Line` is a `vector<char>`. For example:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_767_0.png)

Now, when we inserted that **t**, we only had to move the rest of the characters on that line. Furthermore, when we need to, we can add a new line without moving any characters. For example, we could insert **This is a new line.** after **document.** to get

```
This is the start of a very long document.
This is a new line.
There are lots of . . .
```

All we needed to do was to insert a new “line” in the middle:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_767_1.png)

The logical reason that it is important to be able to insert new links in a list without moving existing links is that we might have iterators pointing to those links or pointers (and references) pointing to the objects in those links. Such iterators and pointers are unaffected by insertions or deletions of lines. For example, a word processor may keep a `vector<list<Line>::iterator>` holding iterators to the beginning of every title and subtitle in the current `Document`:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_768_0.png)

We can add lines to “paragraph 20.2” without invalidating the iterator to “paragraph 20.3.”

In conclusion, we use a **list** of lines rather than a **vector** of lines or a **vector** of all the characters for both logical and performance reasons. Please note that situations where these reasons apply are rather rare so that the “by default, use **vector**” rule of thumb still holds. You need a specific reason to prefer a **list** over a **vector** – even if you think of your data as a list of elements! (See §20.7) A list is a logical concept that you can represent in your program as a (linked) **list** or as a **vector**. The closest STL analog to our everyday concept of a list (e.g., a to-do list, a list of groceries, or a schedule) is a sequence, and most sequences are best represented as **vectors**.

### 20.6.1 Lines

How do we decide what’s a “line” in our document? There are three obvious choices:

1. Rely on newline indicators (e.g., `\n`) in user input.
2. Somehow parse the document and use some “natural” punctuation (e.g., .).
3. Split any line that grows beyond a given length (e.g., 50 characters) into two.

There are undoubtedly also some less obvious choices. For simplicity, we use alternative 1 here.

We will represent a document in our editor as an object of class **Document**. Stripped of all refinements, our document type looks like this:

```cpp
using Line = vector<char>;        // a line is a vector of characters

struct Document {
    list<Line> line;              // a document is a list of lines
    Document() { line.push_back(Line{}); }
};
```

Every **Document** starts out with a single empty line: **Document’s** constructor makes an empty line and pushes it into the list of lines. Reading and splitting into lines can be done like this:

```cpp
istream& operator>>(istream& is, Document& d)
{
    for (char ch; is.get(ch); ) {
        d.line.back().push_back(ch);        // add the character
        if (ch=='\n')
            d.line.push_back(Line{});       // add another line
    }
    if (d.line.back().size()) d.line.push_back(Line{}); // add final empty line
    return is;
}
```

Both **vector** and **list** have a member function **back()** that returns a reference to the last element. To use it, you have to be sure that there really is a last element for **back()** to refer to – don’t use it on an empty container. That’s why we defined a **Document** to end with an empty **Line**. Note that we store every character from input, even the newline characters (`"\n"`). Storing those newline characters greatly simplifies output, but you have to be careful how you define a character count (just counting characters will give a number that includes space and newline characters).

### 20.6.2 Iteration

If the document was just a `vector<char>` it would be simple to iterate over it. How do we iterate over a list of lines? Obviously, we can iterate over the list using `list<Line>::iterator`. However, what if we wanted to visit the characters one after another without any fuss about line breaks? We could provide an iterator specifically designed for our **Document:**

```cpp
class Text_iterator {  // keep track of line and character position within a line
    list<Line>::iterator ln;
    Line::iterator pos;
public:
    // start the iterator at line ll's character position pp:
    Text_iterator(list<Line>::iterator ll, Line::iterator pp)
        :ln(ll), pos(pp) { }

    char& operator*() { return *pos; }
    Text_iterator& operator++();
    bool operator==(const Text_iterator& other) const;
    bool operator!=(const Text_iterator& other) const;
};
```

```cpp
bool Text_iterator::operator==(const Text_iterator& other) const
{
    return ln==other.ln && pos==other.pos;
}
bool Text_iterator::operator!=(const Text_iterator& other) const
{
    return !(*this==other);
}
```

```cpp
Text_iterator& Text_iterator::operator++()
{
    ++pos; // proceed to next character
    if (pos==(*ln).end()) {
        ++ln; // proceed to next line
        pos = (*ln).begin(); // bad if ln==line.end(); so make sure it isn't
    }
    return *this;
}
```

To make `Text_iterator` useful, we need to equip class **Document** with conventional **begin()** and **end()** functions:

```cpp
struct Document {
    list<Line> line;
    Text_iterator begin() // first character of first line
    {
        return Text_iterator(line.begin(), (*line.begin()).begin());
    }
    Text_iterator end() // one beyond the last character of the last line
    {
        auto last = line.end();
        --last; // we know that the document is not empty
        return Text_iterator(last, (*last).end());
    }
};
```

We need the curious `(*line.begin()).begin()` notation because we want the beginning of what `line.begin()` points to; we could alternatively have used `line.begin()->begin()` because the standard library iterators support `->`.

We can now iterate over the characters of a document like this:

```cpp
void print(Document& d)
{
    for (auto p : d) cout << p;
}

print(my_doc);
```
