# 4.5.3  Pitfalls with References

When dealing with indirect access, we operate with two objects: the proper object and a link object to it in the form of a reference or a pointer to the former. But in some situations, there can be a link (a reference) that refers to a nonexistent object. Consider the following code:

```
```cpp
// Very nasty error - a function returns a reference
// to an object which was destroyed.
// "returning address of local variable or temporary: char_counter_vec"
vector< int > &    CountCharsIn( const string & fileName )
{

    vector< int >    char_counter_vec;

    // open the file, read line by line
    // count chars and push them back to char_counter_vec
    // ...

    // finally, return the counted results

    assert( false );             // do NOT use this code

    return char_counter_vec;     // WRONG!! char_counter_vec will be destroyed
                                 // since it is local to this function
}
```
```

The problem arises in the last line – a reference to the char_counter_vec object is returned. However, since char_counter_vec is a local object, it is automatically destroyed after leaving the function on line [19]. The rref will not help in this respect, either. Thus, anyone who wants to use that object will be in trouble:

```
```cpp
void CountCharsIn_Test( void )
{
    const string fileName( "Test.txt" );

    vector< int >    v = CountCharsIn( fileName );    // serious error lurks here ...

    // display results ...

}
```
```

There are a few solutions to this situation, of which the following is also the simplest. Return a copy of the char_counter_vec vector.

```
```cpp
// Return a copy (or move)
vector< int >   CountCharsIn_copy_( const string & fileName )
{

    vector< int >      char_counter_vec;

    // open the file, read line by line
    // count chars and push them back to char_counter_vec
    // ...

    // finally, return the counted results

    return char_counter_vec;     // OK, char_counter_vec can be copied (in effect it
                                  // will be moved since std::vector is smart enough)
}
```
```