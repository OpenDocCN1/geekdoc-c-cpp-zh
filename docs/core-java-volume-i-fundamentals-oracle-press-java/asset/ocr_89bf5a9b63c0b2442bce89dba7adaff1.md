mix-ins) may supply auxiliary characteristics. That style is similar to a Java class with a single superclass and additional interfaces.

# TIP:

You have seen the `CharSequence` interface in [chapter 3]. Both `String` and `StringBuilder` (as well as a few more esoteric string-like classes) implement this interface. The interface contains methods that are common to all classes that manage sequences of characters. A common interface encourages programmers to write methods that use the `CharSequence` interface. Those methods work with instances of `String`, `StringBuilder`, and the other string-like classes.

Sadly, the `CharSequence` interface is rather paltry. You can get the length, iterate over the code points or code units, extract subsequences, and lexicographically compare two sequences. Java 17 adds an `isEmpty` method.

If you process strings, and those operations suffice for your tasks, accept `CharSequence` instances instead of strings.

# 6.1.4 Static and Private Methods

As of Java 8, you are allowed to add static methods to interfaces. There was never a technical reason why this should be outlawed. It simply seemed to be against the spirit of interfaces as abstract specifications.

Up to now, it has been common to place static methods in companion classes. In the standard library, you’ll find pairs of interfaces and utility classes such as `Collection`/`Collections` or `Path`/`Paths`.

You can construct a path to a file or directory from a URI, or from a sequence of strings, such as `Paths.get("jdk-17", "conf", "security")`. In Java 11, equivalent methods are provided in the `Path` interface: