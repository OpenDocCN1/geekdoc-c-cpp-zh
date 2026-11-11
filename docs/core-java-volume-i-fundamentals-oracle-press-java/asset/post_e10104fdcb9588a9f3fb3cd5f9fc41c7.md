
- The `TypeVariable` interface, describing type variables (such as `T extends Comparable<? super T>`)
- The `WildcardType` interface, describing wildcards (such as `? super T`)
- The `ParameterizedType` interface, describing generic class or interface types (such as `Comparable<? super T>`)
- The `GenericArrayType` interface, describing generic arrays (such as `T[]`)

Figure 8.5 shows the inheritance hierarchy. Note that the last four subtypes are interfaces—the virtual machine instantiates suitable classes that implement these interfaces.

![](img/0e7b74ef51a065c077b42cd87b362288_696_0.png)

**Figure 8.5** The Type interface and its descendants

Listing 8.4 uses the generic reflection API to print out what it discovers about a given class. If you run it with the `Pair` class, you get this report:

```java
class Pair<T> extends java.lang.Object
public T getFirst()
public T getSecond()
public void setFirst(T)
public void setSecond(T)
```

If you run it with `ArrayAlg` in the `PairTest2` directory, the report displays the following method:

```java
public static <T extends java.lang.Comparable> Pair<T> minmax(T[])
```

## Listing 8.4 `genericReflection/GenericReflectionTest.java`

```java
package genericReflection;

import java.lang.reflect.*;
import java.util.*;

/**
 * @version 1.12 2021-05-30
 * @author Cay Horstmann
 */
public class GenericReflectionTest
{
   public static void main(String[] args)
   {
      // read class name from command line args or user input
      String name;
      if (args.length > 0) name = args[0];
      else
      {
         try (var in = new Scanner(System.in))
         {
            System.out.println("Enter class name (e.g., java.util.Collections): ");
            name = in.next();
         }
      }

      try
      {
         // print generic info for class and public methods
         Class<?> cl = Class.forName(name);
         printClass(cl);
         for (Method m : cl.getDeclaredMethods())
            printMethod(m);
      }
      catch (ClassNotFoundException e)
      {
         e.printStackTrace();
      }
   }

   public static void printClass(Class<?> cl)
   {
      System.out.print(cl);
      printTypes(cl.getTypeParameters(), "<", ", ", ">", true);
      Type sc = cl.getGenericSuperclass();
      if (sc != null)
      {
         System.out.print(" extends ");
         printType(sc, false);
      }
      printTypes(cl.getGenericInterfaces(), " implements ", ", ", "", false);
      System.out.println();
   }

   public static void printMethod(Method m)
   {
      String name = m.getName();
      System.out.print(Modifier.toString(m.getModifiers()));
      System.out.print(" ");
      printTypes(m.getTypeParameters(), "<", ", ", ">", true);
      printType(m.getGenericReturnType(), false);
      System.out.print(" ");
      System.out.print(name);
      System.out.print("(");
      printTypes(m.getGenericParameterTypes(), "", ", ", "", false);
      System.out.println(")");
   }

   public static void printTypes(Type[] types, String pre,
         String sep, String suf,
         boolean isDefinition)
   {
      if (pre.equals(" extends ") && Arrays.equals(types, new Type[] { Object.class }))
         return;
      if (types.length > 0) System.out.print(pre);
      for (int i = 0; i < types.length; i++)
      {
         if (i > 0) System.out.print(sep);
         printType(types[i], isDefinition);
      }
      if (types.length > 0) System.out.print(suf);
   }

   public static void printType(Type type, boolean isDefinition)
   {
      if (type instanceof Class t)
      {
         System.out.print(t.getName());
      }
      else if (type instanceof TypeVariable t)
      {
         System.out.print(t.getName());
         if (isDefinition)
            printTypes(t.getBounds(), " extends ", " & ", "", false);
      }
      else if (type instanceof WildcardType t)
      {
         System.out.print("?");
         printTypes(t.getUpperBounds(), " extends ", " & ", "", false);
         printTypes(t.getLowerBounds(), " super ", " & ", "", false);
      }
      else if (type instanceof ParameterizedType t)
      {
         printType(t.getRawType(), false);
         printTypes(t.getActualTypeArguments(), "<", ", ", ">", false);
      }
      else if (type instanceof GenericArrayType t)
      {
         printType(t.getGenericComponentType(), false);
         System.out.print("[]");
      }
   }
}
```

```java
var type = new TypeLiteral<ArrayList<Integer>>() {} // note the {}
```

The TypeLiteral constructor captures the generic supertype:

```java
class TypeLiteral
{
    public TypeLiteral()
    {
        Type parentType = getClass().getGenericSuperclass();
        if (parentType instanceof ParameterizedType paramType)
            type = paramType.getActualTypeArguments()[0];
        else
            throw new UnsupportedOperationException(
                "Construct as new TypeLiteral<...>(){}");
    }
    . . .
}
```

If we have a generic type available at runtime, we can match it against the `TypeLiteral`. We can’t get a generic type from an object—it is erased. But, as you have seen in the preceding section, generic types of fields and method parameters survive in the virtual machine.

Injection frameworks such as CDI and Guice use type literals to control injection of generic types. The example program in the book’s companion code shows a simpler example. Given an object, we enumerate its fields, whose generic types are available, and look up associated formatting actions.

We format an `ArrayList<Integer>` by separating the values with spaces, an `ArrayList<Character>` by joining the characters to a string. Any other array lists are formatted by `ArrayList.toString`.

## Listing 8.5 `genericReflection/TypeLiterals.java`

```java
package genericReflection;

import java.lang.reflect.*;
import java.util.*;
import java.util.function.*;

class TypeLiteral<T>
{
    private Type type;

    public TypeLiteral()
    {
        Type parentType = getClass().getGenericSuperclass();
        if (parentType instanceof ParameterizedType paramType)
            type = paramType.getActualTypeArguments()[0];
        else
            throw new UnsupportedOperationException(
                "Construct as new TypeLiteral<...>(){}");
    }

    private TypeLiteral(Type type)
    {
        this.type = type;
    }

    /**
     * Yields a type literal that describes the given type.
     */
    public static TypeLiteral<?> of(Type type)
    {
        return new TypeLiteral<Object>(type);
    }

    public String toString()
    {
        if (type instanceof Class clazz) return clazz.getName();
        else return type.toString();
    }

    public boolean equals(Object otherObject)
    {
        return otherObject instanceof TypeLiteral otherLiteral
            && type.equals(otherLiteral.type);
    }

    public int hashCode()
    {
        return type.hashCode();
    }
}

/**
 * Formats objects, using rules that associate types with
 * formatting functions.
 */
class Formatter
{
    private Map<TypeLiteral<?>, Function<?, String>> rules = new HashMap<>();

    /**
     * Add a formatting rule to this formatter.
     * @param type The type to which this rule applies
     * @param formatterForType the function that formats objects of this type
     */
    public <T> void forType(TypeLiteral<T> type, Function<T, String> formatterForType)
    {
        rules.put(type, formatterForType);
    }

    /**
     * Formats all fields of an object using the rules of this formatter.
     * @param obj an object
     * @return a string with all field names and formatted values
     */
    public String formatFields(Object obj)
            throws IllegalArgumentException, IllegalAccessException
    {
        var result = new StringBuilder();
        for (Field f : obj.getClass().getDeclaredFields())
        {
            result.append(f.getName());
            result.append("=");
            f.setAccessible(true);
            Function<?, String> formatterForType = rules.get(TypeLiteral.of(f.getGenericType()));
            if (formatterForType != null)
            {
                // formatterForType has parameter type ?. Nothing can be passed to its apply
                // method. Cast makes the parameter type to Object so we can invoke it.
                @SuppressWarnings("unchecked")
                Function<Object, String> objectFormatter
                        = (Function<Object, String>) formatterForType;
                result.append(objectFormatter.apply(f.get(obj)));
            }
            else
                result.append(f.get(obj).toString());
            result.append("\n");
        }
        return result.toString();
    }
}

public class TypeLiterals
{
    public static class Sample
    {
        ArrayList<Integer> nums;
        ArrayList<Character> chars;
        ArrayList<String> strings;

        public Sample()
        {
            nums = new ArrayList<>();
            nums.add(42); nums.add(1729);
            chars = new ArrayList<>();
            chars.add('H'); chars.add('i');
            strings = new ArrayList<>();
            strings.add("Hello"); strings.add("World");
        }
    }

    private static <T> String join(String separator, ArrayList<T> elements)
    {
        var result = new StringBuilder();
        for (T e : elements)
        {
            if (result.length() > 0) result.append(separator);
            result.append(e.toString());
        }
        return result.toString();
    }

    public static void main(String[] args) throws Exception
    {
        var formatter = new Formatter();
        formatter.forType(new TypeLiteral<ArrayList<Integer>>() {},
            lst -> join(" ", lst));
        formatter.forType(new TypeLiteral<ArrayList<Character>>() {},
            lst -> join("", lst));
        System.out.println(formatter.formatFields(new Sample()));
    }
}
```
