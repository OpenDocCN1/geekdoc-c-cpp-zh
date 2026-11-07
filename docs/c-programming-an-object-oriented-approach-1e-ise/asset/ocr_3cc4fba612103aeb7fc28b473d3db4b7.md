The C++ string class is found in the `<string>` header file. It is a class that creates a character array that is not null-terminated and is created in heap memory. It defines data members and member functions like any other class.

# Problems

+   PR-1. The following code fragment uses C strings. Change the code to use C++ strings.

```
```cpp
const char* str = "This is a string.";
cout << strlen (str) << endl;
```
```

+   PR-2. The following code fragment uses C strings. Change the code to use C++ strings.

```
```cpp
const char* str1 = "This is a string.";
const char* str2 = "This is another one";
cout << strcmp (str1, str2) << endl;
```
```

+   PR-3. The following code fragment uses C strings. Rewrite the following code using C++ strings to achieve the same goal.

```
```cpp
char str1 [] = "This is the first string.";
const char* str2 = "Here is another one.";
strcpy (str1, str2);
cout << str1 << endl;
```
```

+   PR-4. The following code fragment uses C strings. Rewrite the code using C++ strings to achieve the same goal.

```
```cpp
char str1 [] = "This is the first string.";
const char* str2 = "Here is another one.";
strncpy (str1, str2, 4);
cout << str1 << endl;
```
```

+   PR-5. The following code fragment uses C strings. Change the code to use C++ strings.

```
```cpp
char str1 [40] = "The time has come. ";
const char* str2 = "Are you ready?";
strcat (str1, str2);
cout << str1 << endl;
```
```

+   PR-6. The following code fragment uses C strings. Change the code to use C++ strings.

```
```cpp
char str1 [40] = "The time has changed. ";
const char* str2 = "Do you know? My dear friend.";
strncat (str1, str2, 12);
cout << str1 << endl;
```
```

+   PR-7. The following code fragment uses C strings. Change the code to use C++ strings.

```
```cpp
char str [] = "This is a long string.";
*strchr (str, 's') = 'S';
*strchr (str, 's') = 'S';
cout << str << endl;
```
```