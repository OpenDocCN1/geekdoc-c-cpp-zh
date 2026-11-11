
> **NOTE:**
>
> Use a static inner class whenever the inner class does not need to access an outer class object. Some programmers use the term *nested class* to describe static inner classes.

> **NOTE:**
>
> Unlike regular inner classes, static inner classes can have static fields and methods.

> **NOTE:**
>
> Classes that are declared inside an interface are automatically `static` and `public`.

> **NOTE:**
>
> Interfaces, records, and enumerations that are declared inside a class are automatically `static`.

[Listing 6.9](#) contains the complete source code of the `ArrayAlg` class and the nested `Pair` class.

**Listing 6.9** `staticInnerClass/StaticInnerClassTest.java`

```java
package staticInnerClass;

/**
 * This program demonstrates the use of static inner classes.
 * @version 1.02 2015-05-12
 * @author Cay Horstmann
 */
public class StaticInnerClassTest
{
   public static void main(String[] args)
   {
      var values = new double[20];
      for (int i = 0; i < values.length; i++)
         values[i] = 100 * Math.random();
      ArrayAlg.Pair p = ArrayAlg.minmax(values);
      System.out.println("min = " + p.getFirst());
      System.out.println("max = " + p.getSecond());
   }
}

class ArrayAlg
{
   /**
    * A pair of floating-point numbers
    */
   public static class Pair
   {
      private double first;
      private double second;

      /**
       * Constructs a pair from two floating-point numbers
       * @param f the first number
       * @param s the second number
       */
      public Pair(double f, double s)
      {
         first = f;
         second = s;
      }

      /**
       * Returns the first number of the pair
       * @return the first number
       */
      public double getFirst()
      {
         return first;
      }

      /**
       * Returns the second number of the pair
       * @return the second number
       */
      public double getSecond()
      {
         return second;
      }
   }

   /**
    * Computes both the minimum and the maximum of an array
    * @param values an array of floating-point numbers
    * @return a pair whose first element is the minimum and whose second element
    * is the maximum
    */
   public static Pair minmax(double[] values)
   {
      double min = Double.POSITIVE_INFINITY;
      double max = Double.NEGATIVE_INFINITY;
      for (double v : values)
      {
         if (min > v) min = v;
         if (max < v) max = v;
      }
      return new Pair(min, max);
   }
}
```

## 6.4 Service Loaders

Sometimes, you develop an application with a service architecture. There are platforms that encourage this approach, such as OSGi ([http://osgi.org](http://osgi.org)), which are used in development environments, application servers, and other complex applications. Such platforms go well beyond the scope of this book, but the JDK also offers a simple mechanism for loading services, described here. This mechanism is well supported by the Java Platform Module System—see [Chapter 9] of Volume II.

Often, when providing a service, a program wants to give the service designer some freedom of how to implement the service’s features. It can also be desirable to have multiple implementations to choose from. The `ServiceLoader` class makes it easy to load services that conform to a common interface.

Define an interface (or, if you prefer, a superclass) with the methods that each instance of the service should provide. For example, suppose your service provides encryption.

```java
package serviceLoader;
public interface Cipher
{
    byte[] encrypt(byte[] source, byte[] key);
    byte[] decrypt(byte[] source, byte[] key);
    int strength();
}
```

The service provider supplies one or more classes that implement this service, for example

```java
package serviceLoader.impl;
public class CaesarCipher implements Cipher
{
    public byte[] encrypt(byte[] source, byte[] key)
    {
        var result = new byte[source.length];
        for (int i = 0; i < source.length; i++)
            result[i] = (byte)(source[i] + key[0]);
        return result;
    }
    public byte[] decrypt(byte[] source, byte[] key)
    {
        return encrypt(source, new byte[] { (byte) -key[0] });
    }
    public int strength() { return 1; }
}
```

The implementing classes can be in any package, not necessarily the same package as the service interface. Each of them must have a no-argument constructor.

Now add the names of the classes to a UTF-8 encoded text file in a file in the `META-INF/services` directory whose name matches the fully qualified interface name. In our example, the file `META-INF/services/serviceLoader.Cipher` would contain the line

```text
serviceLoader.impl.CaesarCipher
```

In this example, we provide a single implementing class. You could also provide multiple classes and later pick among them.

With this preparation done, the program initializes a service loader as follows:

```java
public static ServiceLoader<Cipher> cipherLoader =
    ServiceLoader.load(Cipher.class);
```

This should be done just once in the program.

The iterator method of the service loader returns an iterator through all provided implementations of the service. (See Chapter 9 for more information about iterators.) It is easiest to use an enhanced for loop to traverse them. In the loop, pick an appropriate object to carry out the service.

```java
public static Cipher getCipher(int minStrength)
{
    for (Cipher cipher : cipherLoader) // implicitly calls cipherLoader.iterator()
    {
        if (cipher.strength() >= minStrength) return cipher;
    }
    return null;
}
```

Alternatively, you can use streams (see Chapter 1 of Volume II) to locate the desired service. The stream method yields a stream of ServiceLoader.Provider instances. That interface has methods type and get for getting the provider class and the provider instance. If you select a provider by type, then you just call type and no service instances are unnecessarily instantiated.

```java
public static Optional<Cipher> getCipher2(int minStrength)
{
    return cipherLoader.stream()
        .filter(descr -> descr.type() == serviceLoader.impl.CaesarCipher.class)
        .findFirst()
        .map(ServiceLoader.Provider::get);
}
```

Finally, if you are willing to take any service instance, simply call findFirst:

```java
Optional<Cipher> cipher = cipherLoader.findFirst();
```

The Optional class is explained in Chapter 1 of Volume II.

### `java.util.ServiceLoader<S>` 1.6

- `static <S> ServiceLoader<S> load(Class<S> service)` creates a service loader for loading the classes that implement the given service interface.
- `Iterator<S> iterator()` yields an iterator that lazily loads the service classes. That is, a class is loaded whenever the iterator advances.
- `Stream<ServiceLoader.Provider<S>> stream()` 9 returns a stream of provider descriptors, so that a provider of a desired class can be loaded lazily.
- `Optional<S> findFirst()` 9 finds the first available service provider, if any.

### `java.util.ServiceLoader.Provider<S>` 9

- `Class<? extends S> type()` gets the type of this provider.
- `S get()` gets an instance of this provider.

## 6.5 Proxies

In the final section of this chapter, we discuss *proxies*. You can use a proxy to create, at runtime, new classes that implement a given set of interfaces. Proxies are only necessary when you don’t yet know at compile time which interfaces you need to implement. This is not a common situation for application programmers, so feel free to skip this section if you are not interested in advanced wizardry. However, for certain systems programming applications, the flexibility that proxies offer can be very important.

### 6.5.1 When to Use Proxies

Suppose you want to construct an object of a class that implements one or more interfaces whose exact nature you may not know at compile time. This is a difficult problem. To construct an actual class, you can simply use the `newInstance` method or use reflection to find a constructor. But you can’t instantiate an interface. You need to define a new class in a running program.

To overcome this problem, some programs generate code, place it into a file, invoke the compiler, and then load the resulting class file. Naturally, this is slow, and it also requires deployment of the compiler together with the program. The proxy mechanism is a better solution. The proxy class can create brand-new classes at runtime. Such a proxy class implements the interfaces that you specify. In particular, the proxy class has the following methods:

- All methods required by the specified interfaces; and
- All methods defined in the object class (`toString`, `equals`, and so on).

However, you cannot define new code for these methods at runtime. Instead, you must supply an *invocation handler*. An invocation handler is an object of any class that implements the `InvocationHandler` interface. That interface has a single method:

```java
Object invoke(Object proxy, Method method, Object[] args)
```

Whenever a method is called on the proxy object, the invoke method of the invocation handler gets called, with the Method object and parameters of the original call. The invocation handler must then figure out how to handle the call.

### 6.5.2 Creating Proxy Objects
