# 3.2 Actions

Note that the two reasons that a function might be impure—side effects or dependency on external mutable state—are closely related. Both stem from the notion of mutable state: A function can be impure because of its own mutations, or because it is impacted by the mutations of other functions. In particular, in a program that consists entirely of functions free of side effects, all the functions are pure.³ Mutation is the source of impurity.

Both functions firstString1 and firstString2 return the first string of a list, but firstString2 also removes the string from the list as a side effect. A third variant of the function is possible, one that removes the first string, but does not return it:

```
def removeFirstString(strings: util.List[String]): Unit = strings.remove(0)
```

This function uses the same implementation as firstString2, but its return type is different: Unit instead of String. For a programmer new to functional programming, Unit is an unusual type. There is only one value of type Unit, typically referred to as unit, and represented in Scala by the token “()”.

As a function, removeFirstString is not very useful: From its return type, you already know that the function will return unit before you even call it. So why call it as all? For its side effect of removing the first string from the list.

Type Unit is used when a function has nothing useful to return and is defined solely for the purpose of exploiting its side effects. Such functions are sometimes called procedures. In this book, I use the simpler and shorter term action instead of procedure, but this is not standard terminology. By choosing Unit as the return type, you can make it clear to the user that a function has side effects. Indeed, a function with return type Unit and no side effects would truly be useless.

Several hybrid languages rely on the Unit type to ensure that all methods are functions: Every method returns a value, even if this value is sometimes useless. As an older language, Java uses the notion of void methods, which do not return anything, and thus are not functions, not even peculiar ones. In Java, removeFirstString would be a void method, making it clear that it is invoked only for the purpose of exerting a side effect.

You can make your code less surprising by relying as much as possible on actions and pure functions. Take, for example, class java.util.Arrays. All its methods are either actions like sort or fill or setAll, which modify their input but return no value, or pure functions, like binarySearch or hashCode or equals, which return a new value without side effects.

Functions that include side effects but are not actions, like firstString2, tend to be more confusing. In particular, impurity is not obvious from the function’s signature, since