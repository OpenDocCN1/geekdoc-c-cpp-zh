For an explanation of the C input operations, see §27.6.2 and §B.11.2.

The **realloc()** function may or may not move the old allocation into newly allocated memory. Don’t even think of using **realloc()** on memory allocated by **new**.

Using the C++ standard library, the (roughly) equivalent code is

```
vector<char> buf;
char c;
while (cin.get(c)) buf.push_back(c);
```

Refer to the paper “Learning Standard C++ as a New Language” (see the reference list in §27.1) for a more thorough discussion of input and allocation strategies.

# 27.5 C-style strings

In C, a string (often called a *C string* or a *C-style string* in C++ literature) is a zero-terminated array of characters. For example:

```
char* p = "asdf";
char s[] = "asdf";
```

![](bbox=[0.34, 0.52, 0.75, 0.59])

In C, we cannot have member functions, we cannot overload functions, and we cannot define an operator (such as **==**) for a **struct**. It follows that we need a set of (nonmember) functions to manipulate C-style strings. The C and C++ standard libraries provide such functions in <**string.h**>:

```
size_t strlen(const char* s); // count the characters
char* strcat(char* s1, const char* s2); // copy s2 onto the end of s1
int strcmp(const char* s1, const char* s2); // compare lexicographically
char* strcpy(char* s1, const char* s2); // copy s2 into s1

char* strchr(const char* s, int c); // find c in s
char* strstr(const char* s1, const char* s2); // find s2 in s1

char* strncpy(char*, const char*, size_t n); // strcpy, max n chars
char* strncat(char*, const char*, size_t n); // strcat with max n chars
int strncmp(const char*, const char*, size_t n); // strcmp with max n chars
```