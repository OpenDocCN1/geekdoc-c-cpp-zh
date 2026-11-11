```
```java
SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

private String abbreviation;

private Size(String abbreviation) { this.abbreviation = abbreviation; }
public String getAbbreviation() { return abbreviation; }
}
```
```

The constructor of an enumeration is always private. You can omit the private modifier, as in the preceding example. It is a syntax error to declare an enum constructor as public or protected.

All enumerated types are subclasses of the class `Enum`. They inherit a number of methods from that class. The most useful one is `toString`, which returns the name of the enumerated constant. For example, `Size.SMALL.toString()` returns the string `"SMALL"`.

The converse of `toString` is the static `valueOf` method. For example, the statement

```
```java
Size s = Enum.valueOf(Size.class, "SMALL");
```
```

sets `s` to `Size.SMALL`.

Each enumerated type has a static `values` method that returns an array of all values of the enumeration. For example, the call

```
```java
Size[] values = Size.values();
```
```

returns the array with elements `Size.SMALL`, `Size.MEDIUM`, `Size.LARGE`, and `Size.EXTRA_LARGE`. The `ordinal` method yields the position of an enumerated constant in the enum declaration, counting from zero. For example, `Size.MEDIUM.ordinal()` returns 1.

The short program in Listing 5.12 demonstrates how to work with enumerated types.

> > **NOTE:** The `Enum` class has a type parameter that we have ignored for simplicity. For example, the enumerated type `Size` actually extends `Enum<Size>`. The type parameter is used in the `compareTo` method. (We discuss the `compareTo` method in Chapter 6 and type parameters in Chapter 8.)

**Listing 5.12** `enums/EnumTest.java`

```
```java
1 package enums;
2
3 import java.util.*;
```
```