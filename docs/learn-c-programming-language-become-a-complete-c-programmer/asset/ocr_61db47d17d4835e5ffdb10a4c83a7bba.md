```
};
// uncheckedelement access // add c at end
// forthe shortstr ingoptimization
```

The template<typename C> prefix specifies that a template is being declared and that a type argument C will be used in the declaration. After its introduction, C is used exactly like other type names. The scope of C extends to the end of the declaration prefixed by template<typename C>. You may prefer the shorter and equivalent form template<class C>. In either case, C is a type name; it need not be the name of a class. Mathematicians will recognize template<typename C> as a variant of the traditional “for all C” or more specifically “for all types C” or even “for all C, such that C is a type.” If you think along those lines, you will note that C++ lacks a fully general mechanism for specifying the required properties of a template parameter C. That is, we can’t say “for all C, such that ...” where the “...” is a set of requirements for C. In other words, C++ does not offer a direct way to say what kind of type a template argument C is supposed to be (§24.3).

The name of a class template followed by a type bracketed by<> is the name of a class (as defined by the template) and can be used exactly like other class names. For example:

```
String<char> cs;
String<unsigned char> us;
String<wchar_t> ws;
struct Jchar { /*...*/ }; // Japanese character
```

```
String<Jchar> js;
```

# Section 23.2 A Simple String Template 669

Except for the special syntax of its name, String<char> works exactly as if it had been defined using the definition of class String in §19.3. Making String a template allows us to provide the facilities we had for String of char for Strings of any kind of character. For example, if we use the standardlibrary map and the String template, the word-counting example from §19.2.1 becomes:

```
int main() // count the occurrences of each word on input
{
map<String<char>,int> m;
for (String<char> buf; cin>>buf;)
++m[buf];
// ... write out result ...
}
```

The version for our Japanese-character type Jchar would be:

```
int main() // count the occurrences of each word on input {
map<String<Jchar>,int> m;
for (String<Jchar> buf; cin>>buf;)
++m[buf];
// ... write out result ...
}
```