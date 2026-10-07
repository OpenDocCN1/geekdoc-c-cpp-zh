As you see, the remove() method reduces the list la from 10 elements to 6 elements. However, list lb still contains 10 elements after the remove() function is applied to it. The last 4 elements are disposable because each is either the value 4 or a duplicate of a value moved farther to the front of the list.

Although the methods are usually better suited, the nonmethod functions are more general. As you've seen, you can use them on arrays and string objects as well as STL containers, and you can use them with mixed container types—for example, to save data from a vector to a list or set.

# Using the STL

The STL is a library whose parts are designed to work together. The STL components are tools, but they are also building blocks to create other tools. Let's illustrate this with an example. Suppose you want to write a program that lets the user enter words. At the end, you'll have a record of the words as they were entered, an alphabetical list of the words used (capitalization differences ignored), and a record of how many times each word was entered. To keep things simple, let's assume the input contains numbers or punctuation.

Entering and saving the list of words is simple enough. Following the example of Listings 16.8 and 16.9, you can create a vector<string> object and use push_back() to add words to the vector:

```
vector<string> words;
string input;
while (cin >> input && input != "quit")
words.push_back(input);
```

What about getting the alphabetical word list? You can use sort() followed by unique(), which is an easy way that avoids the original data because sort() is an in-place algorithm. There is another way to create a set<string> object and copy (using an insert iterator) the words from the vector to the set. A set automatically sorts its contents, which means you don't have to call sort(), and a set allows only one copy of a key, so that takes the place of calling unique(). Wait! The specification for ignoring the case differences. One way to handle this is to use transform() instead of copy() to copy data from the vector to the set. For the transformation function, you can use one that converts a string to lowercase:

```
set<string> wordset;
transform(words.begin(), words.end(),
insert_iterator<set<string>>(wordset, wordset.begin()), ToLower);
```

The ToLower() function is easy to write. You can use transform() to apply the toolower() function to each element in the string, using the string as source and destination. Remember, string objects, too, can use the STL functions. Passing and returning the string as a reference means the algorithm works on the original string without having to make copies. Here's the code for ToLower():