In Chapter 2, "Programming in Objective-C," you used several variables to store integer values. For example, you used the variable sum in Program 2.4 to store the result of the addition of the two integers 50 and 25.

The Objective-C language allows you to store data types other than just integers in variables as well, as long as the proper declaration for the variable is made before it is used in the program. Variables can be used to store floating-point numbers, characters, and even objects (or, more precisely, references to objects).

The rules for forming names are quite simple: They must begin with a letter or underscore (_), and they can be followed by any combination of letters (upper- or lowercase), underscores, or the digits 0–9. The following is a list of valid names:

+   * sum
* pieceFlag
* i
* myLocation
* numberOfMoves
* sysFlag
* ChessBoard

On the other hand, the following names are not valid for the stated reasons:

+   * sum$value $—is not a valid character.
* piece flag—Embedded spaces are not permitted.
* 3Spencer—Names can't start with a number.
* int—This is a reserved word.