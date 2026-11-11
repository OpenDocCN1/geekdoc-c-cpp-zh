Can you convert to the raw type and then cause a type error? Unfortunately, you can. Consider this example:

```
var managerBuddies = new Pair<Manager>(ceo, cfo);
Pair rawBuddies = managerBuddies; // OK
rawBuddies.setFirst(new File("...")); // only a compile-time warning
```

This sounds scary. However, keep in mind that you are no worse off than you were with older versions of Java. The security of the virtual machine is not at stake. When the foreign object is retrieved with getFirst and assigned to a Manager variable, a ClassCastException is thrown, just as in the good old days. You merely lose the added safety that generic programming normally provides.

Finally, generic classes can extend or implement other generic classes. In this regard, they are no different from ordinary classes. For example, the class ArrayList<T> implements the interface List<T>. That means an ArrayList<Manager> can be converted to a List<Manager>. However, as you just saw, an ArrayList<Manager> is not an ArrayList<Employee> or List<Employee>. Figure 8.2 shows these relationships.

# 8.8 Wildcard Types

It was known for some time among researchers of type systems that a rigid system of generic types is quite unpleasant to use. The Java designers invented an ingenious (but nevertheless safe) “escape hatch”: the wildcard type. The following sections show you how to work with wildcards.

# 8.8.1 The Wildcard Concept

In a wildcard type, a type parameter is allowed to vary. For example, the wildcard type

```
Pair<? extends Employee>
```

denotes any generic Pair type whose type parameter is a subclass of Employee, such as Pair<Manager>, but not Pair<String>.

Let’s say you want to write a method that prints out pairs of employees, like this:

```
public static void printBuddies(Pair<Employee> p)
{
    Employee first = p.getFirst();
    Employee second = p.getSecond();
    System.out.println(first.getName() + " and " + second.getName() + " are buddies.");
}
```