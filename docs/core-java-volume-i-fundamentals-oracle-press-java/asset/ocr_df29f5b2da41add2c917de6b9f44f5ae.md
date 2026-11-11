```
77    }
78    }
```

# 6.4 Service Loaders

Sometimes, you develop an application with a service architecture. There are platforms that encourage this approach, such as OSGi ([http://osgi.org](http://osgi.org)), which are used in development environments, application servers, and other complex applications. Such platforms go well beyond the scope of this book, but the JDK also offers a simple mechanism for loading services, described here. This mechanism is well supported by the Java Platform Module System—see [Chapter 9] of Volume II.

Often, when providing a service, a program wants to give the service designer some freedom of how to implement the service’s features. It can also be desirable to have multiple implementations to choose from. The `ServiceLoader` class makes it easy to load services that conform to a common interface.

Define an interface (or, if you prefer, a superclass) with the methods that each instance of the service should provide. For example, suppose your service provides encryption.

```
package serviceLoader;
public interface Cipher
{
    byte[] encrypt(byte[] source, byte[] key);
    byte[] decrypt(byte[] source, byte[] key);
    int strength();
}
```

The service provider supplies one or more classes that implement this service, for example

```
package serviceLoader.impl;
public class CaesarCipher implements Cipher
{
```