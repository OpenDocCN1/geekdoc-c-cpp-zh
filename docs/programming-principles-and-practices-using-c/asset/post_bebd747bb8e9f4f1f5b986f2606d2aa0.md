
## Presenting Documents and Iteration

Presenting the document as a sequence of characters is useful for many things, but usually we traverse a document looking for something more specific than a character. For example, here is a piece of code to delete line **n**:

```c++
void erase_line(Document& d, int n)
{
    if (n<0 || d.line.size()-1<=n) return;
    auto p = d.line.begin();
    advance(p,n);
    d.line.erase(p);
}
```

A call **advance(p,n)** moves an iterator **p** **n** elements forward; **advance()** is a standard library function, but we could have implemented it ourselves like this:

```c++
template<typename Iter>    // requires Forward_iterator<Iter>
void advance(Iter& p, int n)
{
    while (0<n) { ++p; --n; }
}
```

Note that **advance()** can be used to simulate subscripting. In fact, for a **vector** called **v**, **p=v.begin**; **advance(p,n)**; **p=x** is roughly equivalent to **v[n]=x**. Note that “roughly” means that **advance()** laboriously moves past the first **n-1** elements one by one, whereas the subscript goes straight to the **nth** element. For a **list**, we have to use the laborious method. It’s a price we have to pay for the more flexible layout of the elements of a **list**.

For an iterator that can move both forward and backward, such as the iterator for **list**, a negative argument to the standard library **advance()** will move the iterator backward. For an iterator that can handle subscripting, such as the iterator for a **vector**, the standard library **advance()** will go directly to the right element rather than slowly moving along using **++**. Clearly, the standard library **advance()** is a bit smarter than ours. That’s worth noticing: typically, the standard library facilities have had more care and time spent on them than we could afford, so prefer the standard facilities to “home brew.”

### TRY THIS

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_771_0.png)

Rewrite **advance()** so that it will “go backward” when you give it a negative argument.

## Search Iteration

Probably, a search is the kind of iteration that is most obvious to a user. We search for individual words (such as **milkshake** or **Gavin**), for sequences of letters that can’t easily be considered words (such as **secret** followed by **homestead** on the next line), for regular expressions (e.g., `[**bB**]\w*\ne` – i.e., an upper- or lowercase **B** followed by 0 or more letters followed by **ne**; see Chapter 23), etc. Let’s show how to handle the second case, finding a string, using our **Document** layout. We use a simple – non-optimal – algorithm:

- Find the first character of our search string in the document.
- See if that character and the following characters match our search string.
- If so, we are finished; if not, we look for the next occurrence of that first character.

For generality, we adopt the STL convention of defining the text in which to search as a sequence defined by a pair of iterators. That way we can use our search function for any part of a document as well as a complete document. If we find an occurrence of our string in the document, we return an iterator to its first character; if we don’t find an occurrence, we return an iterator to the end of the sequence:

```cpp
Text_iterator find_txt(Text_iterator first, Text_iterator last, const string& s)
{ 
    if (s.size()==0) return last;  // can’t find an empty string
    char first_char = s[0];
    while (true) {
        auto p = find(first,last,first_char);
        if (p==last || match(p,last,s)) return p;
        first = ++p;           // look at the next character
    }
}
```

Returning the end of the sequence to indicate “not found” is an important STL convention. The **match()** function is trivial: it just compares two sequences of characters. Try writing it yourself. The **find()** used to look for a character in the sequence of characters is arguably the simplest standard library algorithm (§21.2). We can use our **find_txt()** like this:

```cpp
auto p = find_txt(my_doc.begin(), my_doc.end(), "secret\nhomestead");
if (p==my_doc.end())
    cout << "not found";
else {
    // do something
}
```

## Text Processor Operations

Our "text processor" and its operations are very simple. Obviously, we are aiming for simplicity and reasonable efficiency, rather than at providing a "feature-rich" editor. Don't be fooled into thinking that providing *efficient* insertion, deletion, and search for arbitrary character sequences is trivial, though. We chose this example to illustrate the power and generality of the STL concepts *sequence*, *iterator*, and *container* (such as **list** and **vector**) together with some STL programming conventions (techniques), such as returning the end of a sequence to indicate failure. Note that if we wanted to, we could develop **Document** into an STL container – by providing **Text_iterator**, we have done the key part of representing a **Document** as a sequence of values.

## 20.7 vector, list, and string

Why did we use a **list** for the lines and a **vector** for the characters? More precisely, why did we use a **list** for the sequence of lines and a **vector** for the sequence of characters? Furthermore, why didn't we use a **string** to hold a line?

We can ask a slightly more general variant of this question. We have now seen four ways to store a sequence of characters:

- **char[]** (array of characters)
- **vector<char>**
- **string**
- **list<char>**

How do we choose among them for a given problem? For really simple tasks, they are interchangeable; that is, they have very similar interfaces. For example, given an *iterator*, we can walk through each using **+** and use **\*** to access the characters. If we look at the code examples related to **Document**, we can actually replace our **vector<char>** with **list<char>** or **string** without any logical problems. Such interchangability is fundamentally good because it allows us to choose based on performance. However, before we consider performance, we should look at logical properties of these types: what can each do that the others can't?

- **Elem[]**: Doesn't know its own size. Doesn't have **begin()**, **end()**, or any of the other useful container member functions. Can't be systematically range checked. Can be passed to functions written in C and C-style functions. The elements are allocated contiguously in memory. The size of the array is fixed at compile time. Comparison (**==** and **!=**) and output (**<<**) use the pointer to the first element of the array, not the elements.
- **vector<Elem>**: Can do just about everything, including **insert()** and **erase()**. Provides subscripting. List operations, such as **insert()** and **erase()**, typically involve moving elements (that can be inefficient for large elements and large numbers of elements). Can be range checked. The elements are allocated contiguously in memory. A **vector** is expandable (e.g., use `push_back()`). Elements of a vector are stored (contiguously) in an array. Comparison operators (==, !=, <, <=, >, and >=) compare elements.
- **string**: Provides all the common and useful operations plus specific text manipulation operations, such as concatenation (+ and +=). The elements are guaranteed to be contiguous in memory. A **string** is expandable. Comparison operators (==, !=, <, <=, >, and >=) compare elements.
- **list<Elem>**: Provides all the common and usual operations, except subscripting. We can **insert()** and **erase()** without moving other elements. Needs two words extra (for link pointers) for each element. A **list** is expandable. Comparison operators (==, !=, <, <=, >, and >=) compare elements.

As we have seen (§17.2, §18.6), arrays are useful and necessary for dealing with memory at the lowest possible level and for interfacing with code written in C (§27.1.2, §27.5). Apart from that, **vector** is preferred because it is easier to use, more flexible, and safer.

### TRY THIS

What does that list of differences mean in real code? For each array of **char**, **vector<char>**, **list<char>**, and **string**, define one with the value "Hello", pass it to a function as an argument, write out the number of characters in the string passed, try to compare it to "Hello" in that function (to see if you really did pass "Hello"), and compare the argument to "Howdy" to see which would come first in a dictionary. Copy the argument into another variable of the same type.

### TRY THIS

Do the previous **Try this** for an array of **int**, **vector<int>**, and **list<int>** each with the value {1, 2, 3, 4, 5}.

## 20.7.1 insert and erase

The standard library **vector** is our default choice for a container. It has most of the desired features, so we use alternatives only if we have to. Its main problem is its habit of moving elements when we do list operations (**insert()** and **erase()**); that can be costly when we deal with **vectors** with many elements or **vectors** of large elements. Don’t be too worried about that, though. We have been quite happy
