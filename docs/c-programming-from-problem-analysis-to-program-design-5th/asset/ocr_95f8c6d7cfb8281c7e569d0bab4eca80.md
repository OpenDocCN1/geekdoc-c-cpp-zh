+   b. Write the definition of the default constructor of `xClass` so that the `private` member variables of `xClass` are initialized to 0.

+   c. Write the definition of the member function `two` of `yClass` so that the `private` member variable `a` is initialized to the value of the first parameter of `two`, and the `private` member variable `b` is initialized to the value of the second parameter of `two`.

+   10. Explain the difference between the `private` and `protected` members of a class.

+   11. Explain the difference between the `protected` and `public` members of a class.

+   12. Consider the following class definition:

```
```cpp
class first
{
public:
    void setX();
    void print const();
protected:
    int y;
    void setY(int a);
private:
    int x;
};
```
```

Suppose that `class second` is derived from `class first` using the statement:

```
```cpp
class second: private first
```
```

Determine which member of `class first` are `private`, `protected`, and `public` in `class second`.

+   13. Assume the declaration of Exercise 12. Suppose that `class third` is derived from `class first` using the statement:

```
```cpp
class third: protected first
```
```

Determine which members of `class first` are `private`, `protected`, and `public` in `class third`.

+   14. Assume the declaration of Exercise 12. Suppose that `class fourth` is derived from `class first` using the statement:

```
```cpp
class fourth: public first
```
```

Determine which members of `class first` are `private`, `protected`, and `public` in `class fourth`.

+   15. Assume the declaration of Exercise 12. Suppose that `class fifth` is derived from `class first` using the statement:

```
```cpp
class fifth: first
```
```