strings. (These functions are covered in Lesson 18.) To pass a string to one of these
functions, you pass the array name. The same is true of the string display functions
printf() and puts(), discussed later in the chapter.

You might have noticed that "strings stored in an array" was mentioned a moment ago.
Does this imply that some strings aren't stored in arrays? Indeed it does, and the next
section explains why.

# Strings Without Arrays

From the preceding section, you know that a string is defined by the character array’s
name and a null character. The array’s name is a type char pointer to the beginning of
string. The null marks the string’s end. The actual space occupied by the string in
array is incidental. In fact, the only purpose the array serves is to provide allocated space
for the string.

If you could find some memory storage space without allocating an array? You
could then store a string with its terminating null character instead. A pointer to
t first character could serve to specify the string’s beginning as if the string were
in allocated array. How do you go about finding memory space? There are
t methods: One allocates space for a literal string when the program is compiled,
the other uses the malloc() function to allocate space while the program is executing,
process known as dynamic allocation.

# Allocating String Space at Compilation

The start of a string, as mentioned earlier, is indicated by a pointer to a variable of type
char. You might recall how to declare such a pointer:

```
char *message;
```

This statement declares a pointer to a variable of type char named message. It doesn’t
point to anything, but what if you changed the pointer declaration to read:

```
char *message = "Great Caesar’s Ghost!";
```

When this statement executes, the string Great Caesar’s Ghost! (with a terminating null
character) is stored somewhere in memory, and the pointer message is initialized to point
t the first character of the string. Don’t worry handled automatically by the compiler. When defined, message is a pointer to the string
and can be used as such.

The preceding declaration/initialization is equivalent to the following, and the two
notations *message and message{} also are equivalent; both mean “a pointer to to":