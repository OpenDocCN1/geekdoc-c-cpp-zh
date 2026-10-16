then the call max(2,3) is ambiguous because of the possible implicit conversions from int to double (which could be done either on the first or second parameter). If implicit conversions were not allowed, then the programmer would be forced to specify which conversion is meant. (A second example of this phenomenon was just seen in Ada in the previous section.)

A middle ground between the two extremes of eliminating all implicit conversions and allowing conversions that could potentially be errors is to allow only those implicit conversions that are guaranteed not to corrupt data. For example, Java follows this principle and only permits widening implicit conversions for arithmetic types. C++, too, adopts a more cautious approach than C toward narrowing conversions, generating warning messages in all cases except the int to char narrowing implicit conversion.¹⁶

Even explicit casts need to be restricted in various ways by languages. Often, casts are restricted to simple types, or even to just the arithmetic types. If casts are permitted for structured types, then clearly a restriction must be that the types have identical sizes in memory. The translation then merely reinterprets the memory as a different type, without changing the bit representation of the data. This is particularly true for pointers, which are generally simply reinterpreted as pointing to a value of a different type. This kind of explicit conversion also allows for certain functions, such as memory allocators and deallocators, to be defined using a “generic pointer.” For example, in C the malloc and free functions are declared using the generic or anonymous pointer type void*:

```
void* malloc (size_t );
void free( void*);
```

and casts may be used to convert from any pointer type¹⁷ to void* and back again:

```
int* x = (int*) malloc(sizeof(int));
...
free( (void*)x );
```

Actually, C allows both of these conversions to be implicit, while C++ allows implicit conversions from pointers to void*, but not vice versa.

Object-oriented languages also have certain special conversion requirements, since inheritance can be interpreted as a subtyping mechanism, and conversions from subtypes to supertypes and back are necessary in some cases. This kind of conversion was discussed in more detail in Chapter 5. However, we mention here that C++, because of its mixture of object-oriented and nonobject-oriented features, as well as its compatibility with C, identifies four different kinds of casts, and has invented new syntax for each of these casts: static_cast, dynamic_cast, reinterpret_cast, and const_cast. The first, static_cast, corresponds to the casts we have been describing here¹⁸ (static, since the compiler interprets the cast, generates code if necessary, and the runtime system is not involved). Thus, the previous explicit cast example would be written using the C++ standard as follows:

```
x = static_cast<int>(2.3 + static_cast<double>(x / 2));
```

An alternative to casts is to allow predefined or library functions to perform conversions. For example, in Ada casts between integers and characters are not permitted. Instead, two predefined

> ¹⁶Stroustrup [1994], pp. 41–43, discusses why warnings are not generated in this case.
> ¹⁷Not "pointers to functions," however.
> ¹⁸The reinterpret_cast is not used for void* conversions, but for more dangerous conversions such as char* to int* or int to char*.