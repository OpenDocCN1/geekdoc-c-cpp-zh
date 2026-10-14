Line 12 imports the dice rolling program from Listing E.1. This is probably the most important item in this program; without the dice roller, no results can be made.

Line 14 is a function that calls the dice roller module and returns a value. The value will be used as a character's physical or mental attribute.

Line 20 starts a function that generates a character's hit points, based on individual body parts, e.g. head, arm, torso, etc. This function uses a default value for *body_part*; this way I didn't have to account for every body part individually.

Line 31 is a function to store each attribute. A dictionary is used to link an attribute name to its corresponding value. Each attribute calls the **setAttribute()** function (Line 14) to calculate the value. The completed dictionary is returned when this function is done.

Line 51 shows a “block comment”, a comment I use to describe what a block of related code will be doing. It’s similar to a doc string but is ignored by the Python interpreter. It’s simply there to help the programmer understand what the following lines of code will be doing. The code following the block comment is delimited by a blank line from any non-related code.

Line 55 is a function that puts hit point values into a dictionary, and follows the pattern of **makeAttrib()** (Line 31) function above.

Line 69 is a testing function. When this program is called on its own (not part of another program), such as from the command line, it will make a sample character and print out the values to show that the program is working correctly. Line 78 has the command that determines whether the **test()** function will run or not.

# # E.4 Text-based character creation

The next few pages (Listing E.4) are a console-based (non-graphical) character creation program that I wrote shortly after the attribute generator above. This was the basis for a game I was making based on the Colonial Marines from the Aliens movie. It’s not perfect, barely complete enough for real use, but it is useful for several reasons:

+   1. It’s object-oriented, showing how inheritance, “self”, and many of the other features of OOP actually work in practice.