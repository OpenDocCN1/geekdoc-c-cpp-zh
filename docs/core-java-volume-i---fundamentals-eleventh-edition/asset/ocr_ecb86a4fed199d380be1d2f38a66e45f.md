```
~~~java
        new Timer(1000, listener).start();
    }
}
~~~
```

The rule is that any captured variable in a lambda expression must be *effectively final*. An effectively final variable is a variable that is never assigned a new value after it has been initialized. In our case, text always refers to the same String object, and it is OK to capture it. However, the value of i is mutated, and therefore i cannot be captured.

The body of a lambda expression has *the same scope as a nested block*. The same rules for name conflicts and shadowing apply. It is illegal to declare a parameter or a local variable in the lambda that has the same name as a local variable.

```
~~~java
Path first = Path.of("/usr/bin");
Comparator<String> comp
   = (first, second) -> first.length() - second.length();
// ERROR: Variable first already defined
~~~
```

Inside a method, you can't have two local variables with the same name, and therefore, you can't introduce such variables in a lambda expression either. When you use this keyword in a lambda expression, you refer to the this parameter of the method that creates the lambda. For example, consider

```
~~~java
public class Application
{
   public void init()
   {
      ActionListener listener = event ->
         {
            System.out.println(this.toString());
            ...
         };
      ...
   }
}
~~~
```

The expression this.toString() calls the toString method of the Application object, *not* the ActionListener instance. There is nothing special about the use of this in a lambda expression. The scope of the lambda expression is nested inside the init method, and this has the same meaning anywhere in that method.

# ### 6.2.7 Processing Lambda Expressions

Up to now, you have seen how to produce lambda expressions and pass them to a method that expects a functional interface. Now let us see how to write methods that can consume lambda expressions.