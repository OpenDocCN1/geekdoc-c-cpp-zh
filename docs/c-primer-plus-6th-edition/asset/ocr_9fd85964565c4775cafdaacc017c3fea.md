# The New, Improved String Class

# The New, Improved String Class

Now that we are a bit wiser, we can revise the StringBad class, renaming it. First, add the constructor and the assignment operator just discussed so that the class correctly manages the memory used by class objects. Now that you've seen when objects are constructed and destroyed, we can mute the class constructors and destructors so that they no longer announce each time they are used. And now that you're no longer watching the constructors at each time, we can simplify the default constructor so that it constructs an empty string instead of "++".

Next, we can add a few capabilities to the class. A useful class would incorporate all the functionality of the standard library of string functions, but we'll add only enough to see what happens (Keep in mind that this String is an illustrative example and the C++ standard string is much more extensive). In particular, we'll add the following methods:

```
int length() const { return len; }
riend bool operator(const String &st, const String &st2);
friend bool operator(const String &st1, const String &st2);
friend bool operator==(const String &st, const String &st2);
friend operator>>=(istream & is, String & st);
char & operator[](int i);
const char &operator[](int i) const;
static int HowMany();
```

The first new method returns the length of the stored string. The next three functions allow you to compare strings. The operator() function provides simple capabilities. The two operator[] functions provide array-notation access to individual characters in a string. The static class method HowMany() complements the static data member num_strings. Let's look at some details.

# The Revised Default Constructor

The new default constructor merits notice. It looks like this:

```
{
  len = 0;
  str = new char[1];
  str[0] = '\0';      // default string
}
```

You might wonder why the code uses

```
str = new char[1];
```

and not this:

```
str = new char;
```