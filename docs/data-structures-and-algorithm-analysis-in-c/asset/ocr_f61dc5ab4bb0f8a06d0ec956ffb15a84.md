In C++11, an **lvalue reference** is declared by placing an & after some type. An lvalue reference then becomes a synonym (i.e., another name) for the object it references. For instance,

```
string str = "hello";
string & rstr = str; // rstr is another name for str
rstr += "o"; // changes str to "hello"
bool cond = (rstr == &rstr); // true; str and rstr are same object
string & bad1 = "hello"; // Illegal: "hello" is not a modifiable lvalue
string & bad2 = str + ""; // Illegal: str+"" is not an lvalue
string & sub = str.substr( 0, 4 ); // Illegal: str.substr( 0, 4 ) is not an lvalue
```

In C++11, an **rvalue reference** is declared by placing an && after some type. An rvalue reference has the same characteristics as an lvalue reference except that, unlike an lvalue reference, an rvalue reference can also reference an rvalue (i.e., a temporary). For instance,

```
string str = "hello";
string && bad1 = "hello"; // Legal
string && bad2 = str + ""; // Legal
string && sub = str.substr( 0, 4 ); // Legal
```

Whereas lvalue references have several clear uses in C++, the utility of rvalue references is not obvious. Several uses of value references will be discussed now; rvalue references are deferred until Section 1.5.3.

# lvalue references use #1: aliasing complicated names

The simplest use, which we will see in Chapter 5, is to use a local reference variable solely for the purpose of renaming an object that is known by a complicated expression. The code we will see is similar to the following:

```
auto & whichList = theLists[ myhash( x, theLists.size( ) ) ];
if ( find( begin( whichList ), end( whichList ), x ) == end( whichList ) )
    return false;
whichList.push_back( x );
```

A reference variable is used so that the considerably more complex expression theLists[myhash(x,theLists.size())] does not have to be written (and then evaluated) four times. Simply writing

```
auto whichList = theLists[ myhash( x, theLists.size( ) ) ];
```

would not work; it would create a copy, and then the push_back operation on the last line would be applied to the copy, not the original.

# lvalue references use #2: range for loops

A second use is in the range for statement. Suppose we would like to increment by 1 all values in a vector. This is easy with a for loop:

```
for( int i = 0; i < arr.size( ); ++i )
    ++arr[ i ];
```