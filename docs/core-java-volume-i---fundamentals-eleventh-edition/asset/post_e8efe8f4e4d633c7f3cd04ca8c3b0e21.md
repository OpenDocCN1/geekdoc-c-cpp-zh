
```java
public boolean equals(Object otherObject)
{
    if (!super.equals(otherObject)) return false;
    var other = (Manager) otherObject;
    // super.equals checked that this and other belong to the same class
    return bonus == other.bonus;
}

public int hashCode()
{
    return java.util.Objects.hash(super.hashCode(), bonus);
}

public String toString()
{
    return super.toString() + "[bonus=" + bonus + "]";
}
```

- **java.lang.Object 1.0**
  - `Class getClass()`  
    returns a class object that contains information about the object. As you will see later in this chapter, Java has a runtime representation for classes that is encapsulated in the Class class.
  - `boolean equals(Object otherObject)`  
    compares two objects for equality; returns true if the objects point to the same area of memory, and false otherwise. You should override this method in your own classes.
  - `String toString()`  
    returns a string that represents the value of this object. You should override this method in your own classes.

- **java.lang.Class 1.0**
  - `String getName()`  
    returns the name of this class.
  - `Class getSuperclass()`  
    returns the superclass of this class as a Class object.

## 5.3 Generic Array Lists

In some programming languages—in particular, in C and C++—you have to fix the sizes of all arrays at compile time. Programmers hate this because it forces them into uncomfortable tradeoffs. How many employees will be in a department? Surely no more than 100. What if there is a humongous department with 150 employees? Do we want to waste 90 entries for every department with just 10 employees?

In Java, the situation is somewhat better. You can set the size of an array at runtime.

```java
int actualSize = ...;
var staff = new Employee[actualSize];
```

Of course, this code does not completely solve the problem of dynamically modifying arrays at runtime. Once you set the array size, you cannot change it easily. Instead, in Java you can deal with this common situation by using another Java class, called `ArrayList`. The `ArrayList` class is similar to an array, but it automatically adjusts its capacity as you add and remove elements, without any additional code.

`ArrayList` is a generic class with a type parameter. To specify the type of the element objects that the array list holds, you append a class name enclosed in angle brackets, such as `ArrayList<Employee>`. You will see in Chapter 8 how to define your own generic class, but you don’t need to know any of those technicalities to use the array list type.

The following sections show you how to work with array lists.

### 5.3.1 Declaring Array Lists

Here is how to declare and construct an array list that holds `Employee` objects:

```java
ArrayList<Employee> staff = new ArrayList<Employee>();
```

As of Java 10, it is a good idea to use the `var` keyword to avoid duplicating the class name:

```java
var staff = new ArrayList<Employee>();
```

If you don’t use the `var` keyword, you can omit the type parameter on the right-hand side:

```java
ArrayList<Employee> staff = new ArrayList<>();
```

This is called the “diamond” syntax because the empty brackets `<>` resemble a diamond. Use the diamond syntax together with the `new` operator. The compiler checks what happens to the new value. If it is assigned to a variable, passed into a method, or returned from a method, then the compiler checks the generic type of the variable, parameter, or method. It then places that type into the `<>`. In our example, the new `ArrayList<>` is assigned to a variable of type `ArrayList<Employee>`. Therefore, the generic type is `Employee`.

> **CAUTION:** If you declare an `ArrayList` with `var`, do not use the diamond syntax.
>
> The declaration
>
> ```java
> var elements = new ArrayList<>();
> ```
>
> yields an `ArrayList<Object>`.

> **NOTE:** Before Java 5, there were no generic classes. Instead, there was a single `ArrayList` class, a one-size-fits-all collection holding elements of type `Object`. You can still use `ArrayList` without a `<...>` suffix. It is considered a “raw” type, with the type parameter erased.

> **NOTE:** In even older versions of Java, programmers used the `Vector` class for dynamic arrays. However, the `ArrayList` class is more efficient, and there is no longer any good reason to use the `Vector` class.

Use the `add` method to add new elements to an array list. For example, here is how you populate an array list with `Employee` objects:

```java
staff.add(new Employee("Harry Hacker", . . .));
staff.add(new Employee("Tony Tester", . . .));
```

The array list manages an internal array of object references. Eventually, that array will run out of space. This is where array lists work their magic: If you call `add` and the internal array is full, the array list automatically creates a bigger array and copies all the objects from the smaller to the bigger array.

If you already know, or have a good guess, how many elements you want to store, call the `ensureCapacity` method before filling the array list:

```java
staff.ensureCapacity(100);
```

That call allocates an internal array of 100 objects. Then, the first 100 calls to `add` will not involve any costly reallocation.

You can also pass an initial capacity to the `ArrayList` constructor:

```java
ArrayList<Employee> staff = new ArrayList<>(100);
```

> **CAUTION:** Allocating an array list as
>
> ```java
> new ArrayList<>(100) // capacity is 100
> ```
>
> is not the same as allocating a new array as
>
> ```java
> new Employee[100] // size is 100
> ```
>
> There is an important distinction between the capacity of an array list and the size of an array. If you allocate an array list with 100 entries, then the array has 100 slots, ready for use. An array list with a capacity of 100 elements has the *potential* of holding 100 elements (and, in fact, more than 100, at the cost of additional reallocations)—but at the beginning, even after its initial construction, an array list holds no elements at all.

The `size` method returns the actual number of elements in the array list. For example,

```java
staff.size()
```

returns the current number of elements in the `staff` array list. This is the equivalent of

```java
a.length
```

for an array `a`.

Once you are reasonably sure that the array list is at its permanent size, you can call the `trimToSize` method. This method adjusts the size of the memory block to use exactly as much storage space as is required to hold the current number of elements. The garbage collector will then reclaim any excess memory.

Once you trim the size of an array list, adding new elements will move the block again, which takes time. You should only use `trimToSize` when you are sure you won’t add any more elements to the array list.

> **C++ NOTE:** The `ArrayList` class is similar to the C++ `vector` template. Both `ArrayList` and `vector` are generic types. But the C++ `vector` template overloads the `[]` operator for convenient element access. Java does not have operator overloading, so it must use explicit method calls instead. Moreover, C++ vectors are copied by value. If `a` and `b` are two vectors, then the assignment `a = b` makes `a` into a new vector with the same length as `b`, and all elements are copied from `b` to `a`. The same assignment in Java makes both `a` and `b` refer to the same array list.

- **java.util.ArrayList\<E\> 1.2**
  - `ArrayList<>()`  
    constructs an empty array list.
  - `ArrayList<E>(int initialCapacity)`  
    constructs an empty array list with the specified capacity.
  - `boolean add(E obj)`  
    appends `obj` at the end of the array list. Always returns `true`.
  - `int size()`  
    returns the number of elements currently stored in the array list. (Of course, this is never larger than the array list’s capacity.)
  - `void ensureCapacity(int capacity)`  
    ensures that the array list has the capacity to store the given number of elements without reallocating its internal storage array.
  - `void trimToSize()`  
    reduces the storage capacity of the array list to its current size.

### 5.3.2 Accessing Array List Elements

Unfortunately, nothing comes for free. The automatic growth convenience of array lists requires a more complicated syntax for accessing the elements. The reason is that the `ArrayList` class is not a part of the Java programming language; it is just a utility class programmed by someone and supplied in the standard library.

Instead of the pleasant `[]` syntax to access or change the element of an array, you use the `get` and `set` methods.

For example, to set the `i`th element, use

```java
staff.set(i, harry);
```

This is equivalent to

```java
a[i] = harry;
```

for an array `a`. (As with arrays, the index values are zero-based.)
