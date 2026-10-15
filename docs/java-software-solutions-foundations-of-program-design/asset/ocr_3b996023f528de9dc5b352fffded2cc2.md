objects marked for garbage collection and returns their memory to the system for future use. The programmer does not have to worry about explicitly reclaiming memory that has become garbage.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 3.1 What is a null reference?
+   SR 3.2 What does the new operator accomplish?
+   SR 3.3 Write a declaration for a String variable called author, and initialize it to the string "Fred Brooks". Draw a graphic representation of the variable and its value.
+   SR 3.4 Write a code statement that sets the value of an integer variable called size to the length of a String object called name.
+   SR 3.5 What is an alias? How does it relate to garbage collection?

# 3.2 The String Class

Let’s examine the String class in more detail. Figure 3.1 lists some of the more useful methods of the String class.

Once a String object is created, its value cannot be lengthened or shortened, nor can any of its characters change. Thus we say that a String object is immutable. However, several methods in the String class return new String objects that are the result of modifying the original string’s value.

Note that some of the String methods refer to the index of a particular character. A character in a string can be specified by its position, or index, in the string. The index of the first character in a string is zero, the index of the next character is one, and so on. Therefore, in the string "Hello", the index of the character 'H' is zero and the character at index four is 'o'.

Several String methods are exercised in the program shown in Listing 3.1.

As you examine the StringMutation program, keep in mind that this is not a single String object that changes its data; this program creates five separate String objects using various methods of the String class. Originally, the phrase object is set up:

![](bbox=[0.3, 0.88, 0.85, 0.93])