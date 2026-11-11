# Listing 5.14 *(Continued)*

```
```java
48  public static void printConstructors(Class cl)
49  {
50     Constructor[] constructors = cl.getDeclaredConstructors();
51
52     for (Constructor c : constructors)
53     {
54        String name = c.getName();
55        System.out.print("  ");
56        String modifiers = Modifier.toString(c.getModifiers());
57        if (modifiers.length() > 0) System.out.print(modifiers + " ");
58        System.out.print(name + "(");
59
60        // print parameter types
61        Class[] paramTypes = c.getParameterTypes();
62        for (int j = 0; j < paramTypes.length; j++)
63        {
64           if (j > 0) System.out.print(", ");
65           System.out.print(paramTypes[j].getName());
66        }
67        System.out.println(");");
68     }
69  }
70
71  /**
72   * Prints all methods of a class
73   * @param cl a class
74   */
75  public static void printMethods(Class cl)
76  {
77     Method[] methods = cl.getDeclaredMethods();
78
79     for (Method m : methods)
80     {
81        Class retType = m.getReturnType();
82        String name = m.getName();
83
84        System.out.print("  ");
85        // print modifiers, return type and method name
86        String modifiers = Modifier.toString(m.getModifiers());
87        if (modifiers.length() > 0) System.out.print(modifiers + " ");
88        System.out.print(retType.getName() + " " + name + "(");
89
90        // print parameter types
91        Class[] paramTypes = m.getParameterTypes();
```
```