# # VARIABLE KEYWORD ROUNDUP

The C language features a few keywords that puzzle beginners and advanced users alike. Here's the rundown of various variable classifier, quantifier, and what-have-you keywords related to variables.

# **auto**

The auto keyword is a storage class specifier. It's a holdover from the ancient B programming language, which defines all variables used in a function that aren't constants or static. Because this definition means pretty much every variable declaration, the auto variable classification is assumed by the compiler and, therefore, this keyword prefix isn't required.

# **const**

The const keyword is a quantifier used to create a constant or unchanging value. Refer to Chapter 6.

# **enum**

The enum keyword creates an enumerated list of constants. See the section "Enumerating" later in this chapter.

# **extern**

Like auto, the extern keyword is a storage class specifier, referencing variables declared outside of a function. It's covered in Chapter 24, though the concept of external variables are covered elsewhere in this chapter.

# **register**

Another storage class specifier, a variable declared as register (followed by the data type and variable name) is to be stored directly in a CPU register. Modern compilers are highly optimized, which makes this keyword unnecessary.

# **static**

The static keyword declares a storage class that isn't discarded when a function terminates. It's covered elsewhere in this chapter.

# **union**

A union is a complex data construction, similar to a structure. Unlike a structure, the union can hold a variety of data types in the same memory space, though the code can access only one type at a time. Unions are considered a security risk because they define a storage area with an inconsistent data type.

# **volatile**

This scary keyword is a quantifier, often called the opposite of the const keyword. Like register, volatile was once used to optimize code by telling the compiler which variables would change most often. Such optimization is no longer necessary with modern C compilers.