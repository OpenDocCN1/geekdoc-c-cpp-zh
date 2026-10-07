When your program uses complex structures with many members, this notation can be a great time-saver. Other advantages of structures will become apparent as you learn advanced techniques. In general, you will find structures to be useful whenever information of different variable types be treated as a group. For example, in a mailing list database, each entry could be a structure, and each piece of information (name, address, city, and so on) could be a structure member.

Listing 11.1 pulls together everything that has been covered up to this point. It is not practical; however, it illustrates the point of a simple structure.

# Input

LISTING 11.1 simplestruc.c Declaring and Using a Simple Structure

# Output

The coordinates are: (12, 14).

# Analysis

This listing defines a simple structure for holding the coordinates of a point. This is the same structure you've seen illustrated earlier in the lesson. On line 8, the struct keyword is used followed by the tag, coord. The body of the structure is then defined