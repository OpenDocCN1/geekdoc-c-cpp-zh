> > **NOTE:** The following trick, called *double brace initialization*, takes advantage of the inner class syntax. Suppose you want to construct an array list and pass it to a method:
> >
> > ```java
> > var friends = new ArrayList<String>();
> > friends.add("Harry");
> > friends.add("Tony");
> > invite(friends);
> > ```
> >
> > If you don’t need the array list again, it would be nice to make it anonymous. But then how can you add the elements? Here is how:
> >
> > ```java
> > invite(new ArrayList<String>() {{ add("Harry"); add("Tony"); }});
> > ```
> >
> > Note the double braces. The outer braces make an anonymous subclass of `ArrayList`. The inner braces are an object initialization block (see Chapter 4).
> >
> > In practice, this trick is rarely useful. More likely than not, the `invite` method is willing to accept any `List<String>`, and you can simply pass `List.of("Harry", "Tony")`.

> > **CAUTION:** It is often convenient to make an anonymous subclass that is almost, but not quite, like its superclass. But you need to be careful with the `equals` method. In Chapter 5, we recommended that your equals methods use a test
> >
> > ```java
> > if (getClass() != other.getClass()) return false;
> > ```
> >
> > An anonymous subclass will fail this test.

> > **TIP:** When you produce logging or debugging messages, you often want to include the name of the current class, such as
> >
> > ```java
> > System.err.println("Something awful happened in " + getClass());
> > ```
> >
> > But that fails in a static method. After all, the call to `getClass` calls `this.getClass()`, and a static method has no `this`. Use the following expression instead:
> >
> > ```java
> > new Object(){}.getClass().getEnclosingClass() // gets class of static method
> > ```
> >
> > Here, `new Object(){}` makes an anonymous object of an anonymous subclass of `Object`, and `getEnclosingClass` gets its enclosing class—that is, the class containing the static method.

# **Listing 6.8** `anonymousInnerClass/AnonymousInnerClassTest.java`

```
```java
package anonymousInnerClass;
```
```