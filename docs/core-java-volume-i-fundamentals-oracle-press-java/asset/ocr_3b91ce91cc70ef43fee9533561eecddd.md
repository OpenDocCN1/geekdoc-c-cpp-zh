```
```java
12  public static void main(String[] args)
13  {
14      var in = new Scanner(System.in);
15      System.out.print("Enter a size: (SMALL, MEDIUM, LARGE,
    EXTRA_LARGE) ");
16      String input = in.next().toUpperCase();
17      Size size = Enum.valueOf(Size.class, input);
18      System.out.println("size=" + size);
19      System.out.println("abbreviation=" +
    size.getAbbreviation());
20      if (size == Size.EXTRA_LARGE)
21          System.out.println("Good job--you paid attention to
    the __");
22  }
23 }

25 enum Size
26 {
27     SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

29     private Size(String abbreviation) { this.abbreviation =
    abbreviation; }
30     public String getAbbreviation() { return abbreviation; }

32     private String abbreviation;
33 }
```
```

# java.lang.Enum<E> 5

+   - `static Enum valueOf(Class enumClass, String name)`
+   
+     returns the enumerated constant of the given class with the given name.
+   
+   - `String toString()`
+   
+     returns the name of this enumerated constant.
+   
+   - `int ordinal()`