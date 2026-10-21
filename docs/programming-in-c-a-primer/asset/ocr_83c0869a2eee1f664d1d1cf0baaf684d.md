```
new override void display () { }
}
(c) sealed class A {
class B : A
{
...
...
}
```

```
(d) class A {
public class B : A
{
...
...
}
```

```
(e) class A {
class B {
class C: A,B
{
...
...
}
```

```
(f) abstract class XY
{
    abstract Sum (int x, int y) { }
}
```

```
(g) abstract class Print
{
    abstract void Show ( );
}
class Display : Print
{
}
```

```
(h) class A {
public class B
{
    public A Method () { }
}
```

+   13.28 How does a base class receive its arguments in order to construct its members properly?
+   13.29 What happens if a derived class fails to explicitly provide arguments to the base class constructor?
+   13.30 When do we need to use the new modifier on a class declaration?
+   13.31 Distinguish between the inclusion polymorphism and the operation polymorphism.
+   13.32 What is the use of inclusion polymorphism?