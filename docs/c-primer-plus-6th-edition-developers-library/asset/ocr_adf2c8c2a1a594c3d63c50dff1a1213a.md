# Type Conversions

Statements and expressions should normally use variables and constants of just one type. If, however, you mix types, C doesn’t stop dead in its tracks the way, say, Pascal does. Instead, it uses a set of rules to make type conversions automatically. This can be a convenience, but it can also be a danger, especially if you are mixing types inadvertently. (The lint program, found on many Unix systems, checks for type “clashes.” Many non-Unix C compilers report possible type problems if you select a higher error level.) It is a good idea to have at least some knowledge of the type conversion rules.

The basic rules are

+   1. When appearing in an expression, char and short, both signed and unsigned, are automatically converted to int or, if necessary, to unsigned int. (If short is the same size as int, unsigned short is larger than int; in that case, unsigned short is converted to unsigned int.) Under K&R C, but not under current C, float is automatically converted to double. Because they are conversions to larger types, they are called promotions.
+   2. In any operation involving two types, both values are converted to the higher ranking of the two types.
+   3. The ranking of types, from highest to lowest, is long double, double, float, unsigned long long, long long, unsigned long, long, unsigned int, and int. One possible exception is when long and int are the same size, in which case unsigned int outranks long. The short and char types don’t appear in this list because they would have been already promoted to int or perhaps unsigned int.
+   4. In an assignment statement, the final result of the calculations is converted to the type of the variable being assigned a value. This process can result in promotion, as described in rule 1, or demotion, in which a value is converted to a lower-ranking type.
+   5. When passed as function arguments, char and short are converted to int, and float is converted to double. This automatic promotion is overridden by function prototyping, as discussed in Chapter 9, “Functions.”

Promotion is usually a smooth, uneventful process, but demotion can lead to real trouble. The reason is simple: The lower-ranking type may not be big enough to hold the complete number. For instance, an 8-bit char variable can hold the integer 101 but not the integer 22334.

What happens when the converted value won’t fit into the destination? The answer depends on the types involved. Here are the rules for when the assigned value doesn’t fit into the destination type:

+   1. When the destination is some form of unsigned integer and the assigned value is an integer, the extra bits that make the value too big are ignored. For instance, if the destination is 8-bit unsigned char, the assigned value is the original value modulus 256.