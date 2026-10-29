# Pitfall

# COMPILER PROBLEMS

Some compilers have problems with iterator declarations. You can declare an iterator in different ways. For example, we have been using the following:

```
using std::vector<char>::iterator;
. . .
iterator p;
```

Alternatively, you could use the following:

```
std::vector<char>::iterator p;
```

You could also use the following, which is not quite as nice:

```
using namespace std;
. . .
vector<char>::iterator p;
```

There are other similar variations.

Your compiler should accept any of these alternatives. However, we have found that some compilers will accept only certain of these alternatives. If one form does not work with your compiler, try another.

# OTHER KINDS OF ITERATORS

There are other kinds of iterators, which we will not cover in this book. We will briefly mention two kinds of iterators whose names you may encounter. An **input iterator** is essentially a forward iterator that can be used with input streams. An **output iterator** is essentially a forward iterator that can be used with output streams. For more details you will need to consult a more advanced reference.

# Self-Test Exercises

+   5. Suppose the vector `v` contains the letters ‘A’, ‘B’, ‘C’, and ‘D’ in that order. What is the output of the following code?

```
using std::vector<char>::reverse_iterator;
. . .
reverse_iterator i = v.rbegin();
i++; i++;
cout << *i << " ";
i--;
cout << *i << " ";
```