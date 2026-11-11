The following example shows both types of constructors. The first one is a default constructor, and it doesn’t have any parameter. The second constructor has one parameter, the name.

```
```java
public class Kitten {
    public Kitten() {
    }

    public Kitten(String name) {
        // This constructor has one parameter, name.
    }
}
```
```

# Creating Objects

Classes provide the template for objects. Objects are basically created from a class. To create new objects, you will use the ‘new’ keyword.

The following steps are taken to create a new object from a class:

Declaration—This refers to a variable declaration where you will write the name of the variable and its object type.

Instantiation—To create a new object; you will use the ‘new’ keyword.

Initialization—A call to a constructor follows the ‘new’ keyword and initializes a new object.

The following examples show the different steps taken to create a new object from class: