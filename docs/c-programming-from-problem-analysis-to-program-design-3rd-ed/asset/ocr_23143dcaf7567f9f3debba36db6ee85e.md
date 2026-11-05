# QUICK REVIEW

+   1. Instance methods require that an `object` be instantiated before they can be accessed.
+   2. Private members are accessible only within the body of the `class` in which they are declared.
+   3. Often in object-oriented development, data is defined with a `private` modifier, and methods that access the data are declared to have `public` access.
+   4. Methods are the members of a `class` that describe the behavior of the data.
+   5. Many programmers employ the standard convention of using an action verb phrase to name methods.
+   6. Overloaded methods are methods with the same name but a different number, type, or arrangement of parameters. For example, the `doSomething()` method is overloaded with the following headings: `public void doSomething(int x, string y)` and `public void doSomething(string y, int x)`.
+   7. Constructors are special methods that create instances of a `class`. Constructors do not return a value—not even `void`.
+   8. Constructors use the same identifier as the `class` name. The keyword `new` is used to call the constructors.
+   9. When you design a class, you normally use `public` access modifiers with constructors and most other methods and `private` access modifier for data members.
+   10. The default constructor has an empty body and it is automatically created if you do not write one. If you write even one constructor, you lose the default constructor and have to write it.
+   11. Accessors are methods that are used to access a `private` data members. Accessors are also referred to as getter methods.
+   12. Mutators are methods that are used to change the current state of `object` members’ data. Mutator methods are also referred to as setters.
+   13. A property looks like a data field and provides a way to set or get `private` member data. You can define the set without the get or vice versa. It is not necessary to include both.
+   14. To call nonvalue-returning methods, simply type the method’s name. If it is a `static` method, qualify it with the `class` name. If it is an instance method, qualify the identifier with an `object`. If the method has parameters, the call includes actual arguments inside the parentheses, without the types.