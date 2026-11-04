Notice that having the same number of parameters and types is not allowed, even if the return types of the overloading methods are different. For example, if we add a fourth abs() method in class Absolute:

```
public int abs(int a, int b) {
    if(a-b < 0)
        return b-a;
    else
        return a-b;
}
```

the compiler will raise an error message, although it has a different return type.

Unlike C++, Java does not support operator overloading.

# Method Overriding

Java, like C++, supports method overriding; that is, different, but related, classes can declare methods with the same signature, but with different implementations. Unlike method overloading, polymorphism is resolved at runtime (runtime binding), that is, the appropriate method is determined during program execution.

In C++ runtime polymorphism is achieved by using virtual functions and the virtual keyword. This is not required in Java, since all nonstatic methods are virtual functions by default. final methods cannot be overridden, as well as private methods, which cannot be extended, and therefore cannot be overridden. For example, consider the following program:

```
class A {
    public void show() {
        System.out.println("A show()");
    }
}

class B extends A {
    public void show() {
        System.out.println("B show()");
    }
}

class C extends B {
    public void show() {
        System.out.println("C show()");
    }
}

class MainClass {
    public static void main(String[] args) {
        A a = new A();
        B b = new B();
        C c = new C();
    }
}
```