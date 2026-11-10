This is how we declare two variables of type int and long:

```
```
int simply_int;
long simply_long = 50000;
```
```

The last type in the list (long long) has been available with many compilers before it was included in C99. However, Visual Studio supports it only from their 2013 version. In the following sections, we'll examine these types, know their minimum sizes along with the relationship between these sizes.

> Note: The - in -7 is an operator; it multiplies 7 by -1.

# ### 5.6.1 The ANSI Stipulation for Integers

The ANSI standard came into being after C applications had already penetrated the commercial world. In its endeavor to create a standard that also protected these applications, ANSI consciously left the sizes of these data types vague. However, it specified two rules:

+   - A minimum size for the types:
+     short — 2 bytes (16 bits)
+     int — 2 bytes (16 bits)  (Modern int is 4 bytes)
+     long — 4 bytes (32 bits)
+     long long — 8 bytes (64 bits)
+   - A relationship between the types that can be represented in this form:
+     char <= short <= int <= long <= long long

The first rule explains why we used the words “at least” when discussing memory allocation for variables. The second rule implies that a short cannot be smaller than char, an int cannot be smaller than short, and so on. These two rules make it possible for int and long to have the same size on one machine, while short and int may have the same size on another. We included the char data type here because char is essentially an integer type even though it is almost exclusively used to represent characters.

> Takeaway: You can't be assured of seeing a fixed size for any type, but ANSI guarantees a minimum size. It also specifies a relationship between the sizes.

# ### 5.6.2 Signed and Unsigned Integers

By default, the four int types are signed, which means that they can handle both positive and negative integers. This default behavior can be overridden by using the unsigned qualifier before the keyword. For instance, the statement

```
```
unsigned int count;
```
```

allows count to store only positive integers. Because signed data types use one bit to store the sign, the positive side of the range of a signed type is half of its unsigned type (3.3). For instance, the two