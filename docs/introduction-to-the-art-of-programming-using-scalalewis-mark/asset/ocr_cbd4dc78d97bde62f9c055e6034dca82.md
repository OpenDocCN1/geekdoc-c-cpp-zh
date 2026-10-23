```
override def tail = tl
}
```

```
object MyNil extends ImmutableSLList[Nothing] {
  def length = 0
  def apply(index:Int) = throw new IllegalArgumentException("Nil has no contents.")
  override def isEmpty = true
  override def head = throw new IllegalArgumentException("Nil has no head.")
  override def tail = throw new IllegalArgumentException("Nil has no tail.")
}
```

```
object ImmutableSLList {
  def apply[A](data:A*):ImmutableSLList[A] = {
    var ret:ImmutableSLList[A] = MyNil
    for(d <- data.reverse) {
      ret = new Cons(d,ret)
    }
    ret
  }
}
```

There are a few elements of this code that we have not seen before that could use some explanation. Starting at the top, the main class is labeled as sealed and abstract. We have seen abstract before, but sealed is new. What this keyword implies is that all the subtypes of this class have to appear in the current file. This can be used to provide better type checking for patterns in match. In this case it provides us with the security of knowing that other programmers can not produce undesired subtypes that behave in ways different from that desired for our list. Often we can enforce that using final to make sure that nothing inherits from a class. In this case that is not an option as we need to have some inheritance.

Next there is the type parameter for ImmutableSLList. It is +A instead of just A. The plus sign indicates that the list is covariant in the type parameter. This is a topic that is covered in more detail in appendix B. For now it is sufficient to say that this means that if B is a subtype of A then ImmutableSLList[B] is a subtype of ImmutableSLList[A]. Without the plus sign, the type parameters are invariant and the type any different type parameters produce and the type of the class for different type parameters are effectively unrelated.

The first method in the class is called :: to mimic that used in the normal List class. The odd aspect of this is the bounds on the type parameter. This is the first usage we have seen for the >: type bounds. This indicates that we can use any type, B, as long as it the same as A or a supertype of A. This notation was mentioned in subsection 19.4.3, but we did not have a use for it until now. To see the effect that this can have, consider the following code using the standard List in the REPL.

```
scala> val nums = List(1,2,3)
nums: List[Int] = List(1, 2, 3)

scala> "hi" :: nums
res0: List[Any] = List(hi, 1, 2, 3)
```

Note the type of res0. It is a List[Any]. Our list will behave in this same way. The new element, "hi" is not an Int, so Scala has to figure out a type B to use. The only type that is a supertype of both String and Int is Any, so that is what is used. If there were a common supertype lower in the inheritance hierarchy, that would be used instead.

In the iterator method the declaration of rover needs an explicit type because