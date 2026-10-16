In addition to classes, C++ supports a simple form of user-defined type for which we can enumerate the values:

```
enum class Color { red, blue , green };
enum class Traffic_light { green, yellow, red };
Color col = Color::red;
Traffic_light light = Traffic_light::red;
```

Note that enumerators (e.g., red) are in the scope of their enum class, so that they can be used repeatedly in different enum classes without confusion. For example, Color::red is Color’s red which is different from Traffic_light::red.

Enumerations are used to represent small sets of integer values. They are used to make code more readable and less error-prone than it would have been had the symbolic (and mnemonic) enumerator names not been used.

The class after the enum specifies that an enumeration is strongly typed and that its enumerators are scoped. Being separate types, enum classes help prevent accidental misuses of constants. In particular, we cannot mix Traffic_light and Color values:

```
Color x = red; // error : which red?
Color y = Traffic_light::red; // error :that red is not a Color
Color z = Color::red; // OK
```

Similarly, we cannot implicitly mix Color and integer values:

```
int i = Color::red; // error :Color ::redis not an int
Color c = 2; // error :2isnot a Color
```

If you don’t want to explicitly qualify enumerator names and want enumerator values to be ints (without the need for an explicit conversion), you can remove the class from enum class to get a “plain enum” (§8.4.2).

By default, an enum class has only assignment, initialization, and comparisons (e.g., == and <; §2.2.2) defined. However, an enumeration is a user-defined type so we can define operators for it:

# Section 2.3.3 Enumerations 51

```
Traffic_light& operator++(Traffic_light& t) // prefix increment: ++
{
switch (t) {
case Traffic_light::green: return t=Traffic_light::yellow; case Traffic_light::yellow:
return t=Traffic_light::red; case Traffic_light::red: return t=Traffic_light::green; }
}
```

```
Traffic_light next = ++light; // next becomes Traffic_light::green
```

C++ also offers a less strongly typed “plain” enum (§8.4.2).

# 2.4 Modularity

A C++ program consists of many separately developed parts, such as functions (§2.2.1, Chapter 12), user-defined types (§2.3, §3.2, Chapter 16), class hierarchies (§3.2.4, Chapter 20), and templates (§3.4, Chapter 23). The key to managing this is to clearly define the