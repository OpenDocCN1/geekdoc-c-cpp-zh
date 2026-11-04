

```
return f1+f2;
}
public abstract void m3();
}
```

当然，由于类B的m2()方法已经实现，并且覆盖了类A的m2()方法。此外，由于m3()没有实现，因此m3()和B被正确地声明为抽象。那么下面的类C呢？它能成为类B的子类吗？

```
public class C extends B {
    /* 类C的m2()方法覆盖了类B的m2()方法。 */
    public float m2(float f1, float f2) {
        return 2*(f1+f2);
    }
    public final void m3() {
        System.out.println("Hello from Class C!");
    }
}
```

由于方法m3()已经实现，答案是肯定的。它还被声明为final，以防止进一步覆盖。

## 继承

继承是Java和C++以及任何面向对象编程语言最重要的特性之一。在C++部分，我们讨论了继承的优点。简而言之，继承提供了创建新类的能力，新类继承现有类的属性，并且可以添加额外的功能。继承允许我们创建多层次的层级结构。新类称为现有类的派生类或子类，而现有类称为基类、父类或超类。子类可以使用其基类的字段或方法，而无需重写任何代码。定义子类的一般形式是：

```
A_M N_A_M class subclass_name extends base_class_name {
    ... // 子类的构造器、字段和方法。
}
```

A_M和N_A_M分别表示访问修饰符和非访问修饰符。例如，考虑以下程序：

```java
public class Product {
    public String code;
    public double prc;
    public void init(String code, double prc) {
        this.code = code;
        this.prc = prc;
    }
    public void show() {
        System.out.println("\nP:"+ prc + " C:" + code);
    }
}
public class Book extends Product {
    public String title;
    public String auth;
    public int pages;

    public void display() {
        System.out.println("T:"+ title +" A:"+ auth +" P:"+ pages);
    }
}
import java.util.Scanner;
public class MainClass {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        Book b = new Book();

        System.out.print("Price: ");
        b.prc = scan.nextFloat();

        System.out.print("Code: ");
        b.code = scan.next();

        System.out.print("Title: ");
        b.title = scan.next();

        System.out.print("Auth: ");
        b.auth = scan.next();

        System.out.print("Pages: ");
        b.pages = scan.nextInt();

        b.show();
        b.display();
    }
}
```

Book类继承了Product的所有成员。因此，我们不必将Product类的字段和方法复制到Book中。程序读取输入数据，将其存储到相应的字段中，并调用适当的方法来显示数据。给定前面的类，以下程序的输出是什么？

```java
public class MainClass {
    public static void main(String[] args) {
        Product p = new Product();
        Book b = new Book();

        p.init("123-456-789", 40.38);
        b.show();
    }
}
```

实例p与实例b无关。我们故意先调用p的init()方法，然后调用b的show()方法来迷惑你。因此，程序显示b字段的默认值，即：

```
P:0.0 C:null
```

与C++不同，Java只支持单继承，而不支持多继承。换句话说，每个类只有一个直接超类。唯一的例外是java.lang包中的原生类Object，它是唯一没有超类的类。所有没有显式超类的类都派生自Object类。与C++一样，Java支持多级继承。这意味着一个类可以是另一个类的子类，而另一个类又可以是另一个类的子类，以此类推。在这种情况下，一个类继承其所有超类的所有字段和方法。例如：

```
public class Details extends Book {
    public String field;
    public String publisher;
    public int year;
}
```

Details类的实例继承其超类Book和Product的所有字段和方法。

注意，类不继承其超类的构造器，但可以调用它们。类继承其所有超类的所有public和protected字段和方法，无论它们是否在同一个包中。如果它们在同一个包中，它还继承它们的包私有字段和方法，也就是没有访问修饰符的字段和方法。唯一不能被继承，因此不能被访问的字段和方法是声明为private的那些。现在，尝试找出以下程序中的错误：

```java
import java.util.Scanner;

class A {
    private int a;
    protected int x;

    private void show() {
        System.out.println(a);
    }
    public void check_B() {
        System.out.println(k);
    }
}

class B extends A {
    public int k;

    public void display() {
        System.out.println(a + " " + k);
    }
}

class MainClass {
    public static void main(String[] args) {
        B b = new B();
        Scanner scan = new Scanner(System.in);
        System.out.print("Enter number: ");
        b.k = scan.nextInt();
        System.out.print("Enter number: ");
        b.a = scan.nextInt();
        System.out.print("Enter number: ");
        b.x = scan.nextInt();
        b.show();
        b.display();
    }
}
```

由于字段a和方法show()在类A中被声明为private，类B的实例和方法不允许访问它们。因此，以下语句是非法的：

```java
System.out.println(a + " " + k); // 在类B的display()方法中。
b.a = scan.nextInt();
b.show();
```

另一方面，访问public方法check_B()和protected字段x是允许的。但由于字段k是在子类B中声明的，而不是在基类A中，因此以下语句是不可接受的：

```java
System.out.println(k);
```

如前所述，Java不像C++那样支持多继承。我们稍后会看到，Java通过Java接口隐式地支持多继承。

## 多态

与C++一样，Java中的多态是对象具有多种形式的能力，它与重用现有方法名称并赋予它们额外含义的能力相关联。Java和C++一样，提供两种类型的多态：静态多态，在程序编译期间选择适当的方法（静态绑定）；动态多态，在程序执行期间选择适当的方法（运行时绑定）。静态多态的典型示例是方法重载和构造器重载。动态多态的典型示例是方法覆盖。

### 方法重载

Java和C++一样，支持方法重载，即定义具有相同名称的方法的不同版本。每个版本必须具有相同的名称，但参数的数量或类型不同。方法重载的一个示例是我们在讨论构造器时遇到的构造器重载。一旦调用重载方法，编译器会检查参数并选择适当的版本。因此，多态在编译时得到解析。方法重载的优点是不需要为功能相似的方法使用不同的名称。例如，在下一个程序中，类Absolute中的方法abs()被重载了三次。每次调用abs()时，编译器检查参数并调用适当的方法。

```
class Absolute {
    public int abs(int a) {
        if(a < 0)
            return -a;
        else
            return a;
    }
    public double abs(double a) {
        if(a < 0)
            return -a;
        else
            return a;
    }
    public void abs(int a, int b) {
        int sum;
        sum = a+b;
        if(sum < 0)
            System.out.print(-sum);
        else
            System.out.print(sum);
    }
}

class MainClass {
    public static void main(String[] args) {
        int i = -100;
        double j = 1.2345;
        Absolute a = new Absolute();
        System.out.print(a.abs(i) + " ");
        System.out.print(a.abs(j) + " ");
        a.abs(i, 30);
    }
}
```

程序显示：100 1.2345 70

