Why did we first put the **Messages** in a **vector** and then later build a **multimap**? Why didn’t we just put the **Messages** into a **map** immediately? The reason is simple and fundamental:

+   • First, we build a general structure that we can use for many things.
• Then, we use that for a particular application.

That way, we build up a collection of more or less reusable components. Had we immediately built a **map** in the **Mail_file**, we would have had to redefine it whenever we wanted to do some different task. In particular, our **multimap** (significantly called **sender**) is sorted based on the Address field of a message. Most other applications would not find that order particularly useful: they might be looking at Return fields, Recipients, Copy-to fields, Subject fields, time stamps, etc.

This way of building applications in stages (or *layers*, as the parts are sometimes called) can dramatically simplify the design, implementation, documentation, and maintenance of programs. The point is that each part does only one thing and does it in a straightforward way. On the other hand, doing everything at once would require cleverness. Obviously, our “extracting information from an email header” program was just a tiny example of an application. The value of keeping separate things separate, modularization, and gradually building an application increases with size.

To extract information, we simply find all the entries with the key “**John Doe**” using the **equal_range()** function (8.4.10). Then we iterate through all the elements in the sequence [first,second) returned by **equal_range()**, extracting the subject by using **find_subject()**:

```
```cpp
auto pp = sender.equal_range("John Doe <jdoe@machine.example>");

for (auto p = pp.first; p!=pp.second; ++p)
    cout << find_subject(p->second) << '\n';
```
```

When we iterate over the elements of a **map**, we get a sequence of (key,value) pairs, and as with all **pairs**, the first element (here, the **string** key) is called **first** and the second (here, the **Message** value) is called **second** (8.21.6).

# 23.4.1 **Implementation details**

Obviously, we need to implement the functions we use. It was tempting to save a tree by leaving this as an exercise, but we decided to make this example complete. The **Mail_file** constructor opens the file and constructs the **lines** and **m** vectors:

```
```cpp
Mail_file::Mail_file(const string& n)
// open file named n
// read the lines from n into lines
```
```