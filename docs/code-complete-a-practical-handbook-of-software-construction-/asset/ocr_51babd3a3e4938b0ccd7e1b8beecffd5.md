One approach to naming constants is to use a prefix like c_ for constant names. That would give you names like c_RecsMax or c_LinesPerPageMax. In C++ and Java, the convention is to use all uppercase letters, possibly with underscores to separate words, RECSMAX or RECS_MAX and LINESPERPAGEMAX or LINES_PER_PAGE_MAX.

# Identify elements of enumerated types

Elements of enumerated types need to be identified for the same reasons that named constants do—to make it easy to tell that the name is for an enumerated type as opposed to a variable, named constant, or function. The standard approach applies: you can use all caps or an e_ or E_ prefix for the name of the type itself and use a prefix based on the specific type like Color_ or Planet_ for the members of the type.

# Identify input-only parameters in languages that don’t enforce them

Sometimes input parameters are accidentally modified. In languages such as C++ and Visual Basic, you must indicate explicitly whether you want a value that’s been modified to be returned to the calling routine. This is indicated with the *, &, and const qualifiers in C++ or ByRef and ByVal in Visual Basic.

In other languages, if you modify an input variable, it is returned whether you like it or not. This is especially true when passing objects. In Java, for example, all objects are passed “by value,” so when you pass an object to a routine, the contents of the object can be changed within the called routine (Arnold, Gosling, Holmes 2000).

In those languages, if you establish a naming convention in which input-only parameters are given a const prefix (or final, nonmodifiable, or something comparable), you’ll know that an error has occurred when you see anything with a const prefix on the left side of an equal sign. If you see constMax.SetNewMax(...), you’ll know it’s a goof because the const prefix indicates that the variable isn’t supposed to be modified.

Cross-Reference Augmenting a language with a naming convention to make up for limitations in the language itself is an example of programming into a language instead of just programming in it. For more details on programming into a language, see Section 34.4, "Program into Your Language, Not in It."

# Format names to enhance readability

Two common techniques for increasing readability are using capitalization and spacing characters to separate words. For example, GYMNASTICSPOINTTOTAL is less readable than gymnasticsPointTotal or gymnastics_point_total. C++, Java, Visual Basic, and other languages allow for mixed uppercase and lowercase characters. C++, Java, Visual Basic, and other languages also allow the use of the underscore (_) separator.

Try not to mix these techniques; that makes code hard to read. If you make an honest attempt to use any of these readability techniques consistently, however, it will improve your code. People have managed to have zealous, blistering debates over fine points such as whether the first character in a name should be capitalized (TotalPoints vs. totalPoints), but as long as you and your team are consistent, it won’t make much difference. This book uses initial lowercase because of the strength of the Java practice and to facilitate similarity in style across several languages.