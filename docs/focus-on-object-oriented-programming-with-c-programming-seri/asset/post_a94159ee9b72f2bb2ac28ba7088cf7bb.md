
## Reference Arguments

The declaration of reference variables up to now has not really served a very useful purpose. After all, if a variable and an alias for that variable are both defined within the same scope, then why bother to use the alias? Why not just use the name of the variable itself?

The real usefulness of a reference variable occurs when it is created in a scope that is different than the scope of the variable for which it has an alias.

For example, a function sets up a brand new scope whenever it is created. If a reference variable is used as a formal parameter, then it merely becomes an alias for the corresponding actual parameter or argument to the function call. This means that whenever the formal parameter is used within the body of the function, the actual parameter in the calling function is the one that is really being manipulated!

### Simulate Call By Reference

```
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 4, y = 6;
    swap(&x, &y);
    return 0;
}
```

The swap() function:

- declares the function parameter to be a pointer
- uses the dereferenced pointer in the function body
- passes an address as an argument when the function is called

## Call By Reference

```
void swap(int& a, int& b) {
  int temp = a;
  a = b;
  b = temp;
}

int main() {
  int x = 4, y = 6;
  swap(x, y);
  return 0;
}
```

Note that there is no need to dereference a and b. They are automatically dereferenced for us!

### Reference Arguments

Behind the scenes, all references are translated to pointers according to the following two rules:

- whenever a reference variable p is used, replace p by *p
- whenever a reference variable is initialized with a, replace a by &a

The machine code that's generated is exactly the same. We don't have to manually generate the address of a variable. We don't have to create a pointer variable in which to receive the address. This allows the programmer, not the user, to take responsibility for the way the arguments are passed to functions. A reference in C++ is like a pointer because it contains an address, and like an ordinary variable because you don't have to dereference it.

### Constant Reference Parameters

Reference parameters that are used to prevent argument copying (pass by value) and are not intended to change arguments can be declared const to ensure that they do not.

For example:

```
int foo(const bigStruct &bs);
```

This gives you the best of both worlds:

- you can pass arguments efficiently
- you don't have to worry about an argument being changed accidentally

The const prevents the actual parameters from being altered within the function.

Is it always more advantageous to use a pass-by-reference instead of pass-by-value? No. It's just as efficient to pass the actual value of a primitive type as it is to create an alias in the function. When a primitive type variable needs to be used in a function, and no changes need to be made to that variable, pass it by value.

## Inexact Matches Between Actual and Formal Parameters

Consider the following example:

```
int main() {
    int num = 1;
    foo(num);
    cout << "num = " << num << endl;
    return 0;
}

void foo(float& val) {
    ++val;
    cout << "val = " << val << endl;
}

output:
val = 2.00
num = 1
```

Huh???

Integer num is being passed by reference into function foo(), but is received as a reference-to-float, not a reference-to-int. Some compilers will give you a warning message that you may not get the correct results while other compilers will just give a fatal error.

Note that the value of num did not get changed by the function. In order to pass an argument by reference and have the function modify the actual value, there can be no temporary variables created in the process.

For example, if you pass an int by reference and create a float reference to it, then the compiler will convert the int into a temporary float variable and then make the reference to this temporary float via the formal argument. Therefore, if you attempt to modify this float, you would only be modifying the temporary float instead of the actual int argument itself.

## Avoiding a Double Reference by Using Reference Variables

Sometimes in C the address of a pointer variable needs to be passed into a function. In this case the function argument needs to be declared as a pointer to a pointer in order to access the original variable that was being pointed at in the first place.

For example:

```
int main() {
    char *ptr;
    foo(&ptr);
    cout << "ptr = " << ptr << endl;
    return 0;
}

void foo(char **pptr) {
    *pptr = "Hello C++";
}

output:
ptr = Hello C++
```

A better solution is to create a reference variable for this pointer. For example, since the type of the pointer variable ptr is char*, then a reference to it would be type char*&. Therefore, in order to use the actual value of the variable ptr from within the function, no dereferences are required:

```
int main() {
    char *ptr;
    foo(ptr);
    cout << "ptr = " << ptr << endl;
    return 0;
}
```

```
void foo(char*& gptr) {
    gptr = "Hello C++";
}
output:
ptr = Hello C++
```

## Why References Are Essential

Let's look at this class that uses an overloaded addition operator:

```
class Plus {
    private:
        int i;
    public:
        Plus(int x = 0) { i = x; }
        Plus operator+(Plus arg) { return Plus(i + arg.i); }
        void print(char *msg) { cout << msg << endl; }
};

int main() {
    Plus a(13), b(34);
    Plus c;
    c = a + b;
    ...
    return 0;
}
```

The operator+() takes a single argument, which is the value to the right of the + sign. Note that the function is invoked for object on the left of the + sign.

The operator+() function creates a new Plus object by calling the Plus constructor. The argument to the Plus constructor is the sum of the private data parts of the two objects. The Plus constructor creates a new (temporary) Plus object which is copied out of the function as the return value of the operator. Note that all objects are passed and returned by value!

However, there are many occasions when you need to pass the address of an object. For example, objects may be too large to pass by value without destroying the efficiency of the program.

Here is the same class using pointers:

```
class Plus {
private:
    int i;
public:
    Plus(int x = 0) { i = x; }
    Plus operator+(Plus *arg) { return Plus(i + arg->i); }
    void print(char *msg) { cout << msg << endl; }
};

int main() {
    Plus a(13), b(34);
    Plus c;
    c = a + &b;
    return 0;
}
```

The program works but the syntax:

```
a + &b
```

is confusing to say the least! As a last ditch, you could attempt to make the syntax homogeneous:

```
&a + &b
```

This won't work with a member function so you might think it could work with a friend operator+() function instead of a member function. But it doesn't! The C++ compiler must have some way of determining that you want to call the operator+() for a particular class. If you say, &a + &b, the compiler's best guess is that you are adding two pointers!

References allow you to pass addresses to overloaded operator functions and still retain the clear notation of a + b:

```
class Plus {
    private:
        int i;
    public:
        Plus(int x = 0) { i = x; }
        Plus operator+(Plus &arg) { return Plus(i + arg.i); }
        void print(char *msg) { cout << msg << endl; }
};

int main() {
    Plus a(13), b(34);
    Plus c;
    c = a + b;
    return 0;
}
```

With references, you can use operator overloading and still pass addresses when using large objects. This is the reason for the new feature!

You should pass arguments to a function via reference when:

- you want the function to modify the arguments
- the function is not going to modify the arguments but you want to avoid copying the objects to the stack. In this case, use the const qualifier to indicate that the argument being passed by reference will not be altered by the function.
