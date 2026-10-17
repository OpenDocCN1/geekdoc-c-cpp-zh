
- Choose from the following options:
A Add an entry D Delete an entry G Get an entry
List entries Q Quit
Enter a first name: Bill
Enter a second name: Smith
Enter the phone number for Bill Smith: 213 466 6683
Entry successful.

- Choose from the following options:
A Add an entry D Delete an entry G Get an entry
List entries Q Quit
Enter a first name: Mary
Enter a second name: Miller
No entry for Mary Miller

- Choose from the following options:
A Add an entry D Delete an entry G Get an entry
List entries Q Quit
Enter a first name: Mary
Enter a second name: Jones
The number for Mary Jones is 213 443 5671

- Choose from the following options:
A Add an entry D Delete an entry G Get an entry
List entries Q Quit
Enter a first name: Mary
Enter a second name: Jones
Mary Jones erased.

Choose from the following options:
A Add an entry      D Delete an entry      G Get an entry
L List entries      Q Quit

| | | |
|---|---|---|
| Jack Bateman | 312 455 6576 |
| Jane Junket | 413 222 8134 |
| Bill Smith | 213 466 7683 |

Choose from the following options:
A Add an entry      D Delete an entry      G Get an entry
L List entries      Q Quit

# How It Works

You define types for a PhoneBook container and its entries like this:

```cpp
typedef std::map<Person, string> PhoneBook;
typedef std::pair<Person, string> Entry;
```

The object in an entry is a `string` containing phone number, and the key is a `Person` object. These types will make the code easier to read.

You load the map initially in a while loop:

```cpp
while(true) {
    cout << "Do you want to enter a phone book entry(Y or N): ";
    cin >> answer;
    cin.ignore(); // Ignore newline in buffer
    if(toupper(answer) == 'N')
        break;
    if(toupper(answer) != 'Y') {
        cout << "Invalid response. Try again." << endl;
        continue;
    }
    addEntry(phonebook);
}
```

You check whether an entry is to be deleted by reading a character from the input. Reading a character from `cin` leaves a newline in the buffer, which can cause problems for subsequent input. Calling `cin.ignore()` ensures that subsequent input will work properly. If `'n'` or `'N'` is entered, the loop is terminated. If `'y'` or `'Y'` is entered, an entry is created by calling the helper function `addEntry()` which is coded like this:

```cpp
void addEntry(PhoneBook& book) {
    Entry entry = getInput();
    auto pr = book.insert(entry);
    if(pr.second)
        cout << "Entry successful." << endl;
    else
        cout << "Entry exists for " << pr.first->getName() << ". The number is " << pr.first->second << endl;
}
```

The parameter for `addEntry` is a reference. The function modifies the container that is passed as the argument; the function must have access to the original object. In any case, if read-only access to the container was needed, it is important not to allow large objects, such as `map` container, to be passed by value because copying them can severely degrade performance.

An entry is created by calling the helper function which makes use of the `getPerson()` function that creates a `Person` object from the way you saw in the previous section. You then call `insert()` for the `phonebook` object and store the object returned in `pr`. The `pr` enables you to check that the entry was successfully inserted into the map by testing its bool member. The `pr` variable is of `pair<iterator, bool>`, but the `auto` keyword works for you. The first member of `pr` provides access to the entry, whether it is an existing entry or the new entry, and the second is the bool value. You use these to output a message when insertion fails.

After initial input, a while loop provides the mechanism for querying and modifying the book. The switch statement decides the entry to be taken based on the character that is stored in `answer`. Querying the book is managed by the `getEntry()` function:

```cpp
void getEntry(PhoneBook& book) {
    Person person = getPerson();
    auto iter = book.find(person);
    if(iter == book.end())
        cout << "No entry for " << person.getName() << endl;
    else
        cout << "The number for " << person.getName() << " is " << iter->second << endl;
}
```

A `Person` object is created from a name that is read from the keyboard by calling `getPerson()`. The `Person` object is then used as the argument to the `find()` function for the `map` object. This returns an iterator of type `map<Person, string>::const_iterator` that either points to the entry or to one past the last entry in the map. If an entry is found, the second member of the pair pointed to by the iterator provides the number corresponding to the `Person` key.

The `deleteEntry()` deletes an entry from the map. The process is similar to that used in the `getEntry()` function, the difference being that when an entry is found the `erase()` function is called to remove it. You use another version of `erase()` to do this, which the code would look like this:

```cpp
void deleteEntry(PhoneBook& book) {
    Person person = getPerson();
    if(book.erase(person))
        cout << person.getName() << " erased." << endl;
    else
        cout << "No entry found for " << person.getName() << endl;
}
```

The code turns out to be much simpler if you pass the key to the `erase()` function.

The `listEntries()` function lists the contents of a phone book. After an initial check for an empty map, the entries are listed in a range-based for loop. The output is left-justified by the `setflags` manipulator to produce tidy output. This remains in effect until the `resetflags` manipulator is used to restore right-justification.

# Using a Multimap Container

A `multimap` container works much like the `map` container, in that it supports the same range of functions—except for the subscript operator, which you cannot use with a `multimap`. The principle difference between a `map` and a `multimap` is that you can have multiple entries with the same key in a `multimap` and this affects the way some of the functions behave. Obviously, the possibility of several keys having the same value, overloading the operator[] function would not make sense.

When you pass a key to the `erase()` function for a `multimap`, it erases all entries with the same key, and the returned value indicates how many entries were deleted. The significance of having a version of `erase()` that accepts an iterator as an argument should be apparent—it allows you to delete a single element. You also have a version of `erase()` that accepts two iterators to delete a range of entries.

The `find()` function can only find the first element with a given key in a `multimap`. You really need a way to find several elements with the same key and the `lower_bound()`, `upper_bound()`, and `equal_range()` functions provide you with a way to do that. For example, a phonebook object that is of type `multimap<Person, string>`, you could list the phone numbers corresponding to a given key like this:

```cpp
Person person("Jack", "Jones");
auto iter = phonebook.lower_bound(person);
```

```cpp
if(iter == phonebook.end())
    cout << "There are no entries for " << person.getName() << endl;
else
    cout << "The following numbers are listed for " << person.getName() << ":";
    endl;
for( ; iter = phonebook.upper_bound(person); iter++)
    cout << iter->second << endl;
```

检查 `lower_bound()` 返回的迭代器是非常重要的。如果不这样做，你可能会引用到超出最后一个条目的元素。

## 更多迭代器的更多内容

`<iterator>` 头文件定义了从数据源传输数据到目的地的模板。流迭代器（Stream iterators）充当指向输入或输出流的指针，它们允许你在数据流与任何支持迭代器的数据源或目的地（例如算法）之间传输数据。插入迭代器（Insert iterators）可以将数据传输到基础序列容器中。`<iterator>` 头文件定义了流迭代器模板：用于输入流的 `istream_iterator<T>` 和用于输出流的 `ostream_iterator<T>`（其中 T 是要提取或写入的对象类型）；头文件还定义了三个插入模板：`inserter<T>`、`back_inserter<T>` 和 `front_inserter<T>`，其中 T 是数据要插入的序列类型。

让我们更深入地探索其中的一些迭代器：

## 使用输入迭代器

这里有一个如何创建输入迭代器的示例：

```cpp
istream_iterator<int> numbersInput(cin);
```
