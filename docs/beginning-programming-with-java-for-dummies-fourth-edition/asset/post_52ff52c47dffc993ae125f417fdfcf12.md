
Java shapes its input and output to match your computer's locale. Imagine, for example, that your computer runs the version of Windows sold in France. Then, as far as Java is concerned, your computer's locale is Locale.FRANCE, and a run of the code in Listing 18-7 looks like the run shown in Figure 18-11.

**Figure 18-11:** A run of Listing 18-7 on a computer in France.

![](img/6d9dcff12e52b997f3ad31445b712549_379_0.png)

In fact, you can customize your code for many countries, and you don't have to buy airplane tickets to do it! My computer is configured to run in the United States. But in Listing 18-8, I use Java's Locale class to get the run shown in Figure 18-11.

**Listing 18-8: Using a Java Locale**

```java
import java.text.NumberFormat;
import java.util.Locale;
import java.util.Scanner;

class MieuxTraiterLesDonnées {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        keyboard.useLocale(Locale.FRANCE);

        double amount;
        boolean taxable;
        double total;
        NumberFormat currency = NumberFormat.
            getCurrencyInstance(Locale.FRANCE);
        String niceTotal;

        System.out.print("Amount: ");
        amount = keyboard.nextDouble();
        System.out.print("Taxable? (true/false) ");
        taxable = keyboard.nextBoolean();

        if (taxable) {
            total = amount * 1.05;
        } else {
            total = amount;
        }

        niceTotal = currency.format(total);
        System.out.print("Total: ");
        System.out.println(niceTotal);
        keyboard.close();
    }
}
```

## Understanding the Big Picture

In this section, I answer some of the burning questions that I raise throughout the book. "What does java.util stand for?" "Why do I need the word static at certain points in the code?" "How can a degree in Horticultural Studies help you sort cancelled checks?"

I also explain "static" in some unique and interesting ways. After all, static methods and variables aren't easy to understand. It helps to read about Java's static feature from several points of view.

### Packages and import declarations

In Java, you can group a bunch of classes into something called a package. In fact, the classes in Java's standard API are divided into about 200 packages. This book's examples make heavy use of three packages — the packages named java.util, java.lang, and java.io.

### The class java.util.Scanner

The package java.util contains about 50 classes, including the very useful Scanner class. Like most other classes, this Scanner class has two names — a fully qualified name and an abbreviated simple name. The class's fully qualified name is java.util.Scanner, and the class's simple name is Scanner. You get the fully qualified name by adding the package name to the class's simple name. (That is, you add the package name java.util to the simple name Scanner. You get java.util.Scanner.)

An import declaration lets you abbreviate a class's name. With the declaration

```
import java.util.Scanner;
```

the Java compiler figures out where to look for the Scanner class. So instead of writing java.util.Scanner throughout your code, you can just write Scanner.

### The class `java.lang.System`

The package `java.lang` contains about 35 classes, including the ever-popular `System` class. (The class’s fully qualified name is `java.lang.System`, and the class’s simple name is `System`.) Instead of writing `java.lang.System` throughout your code, you can just write `System`. You don’t even need an `import` declaration.

Among all of Java’s packages, the `java.lang` package is special. With or without an import declaration, the compiler imports everything in the `java.lang` package. You can start your program with `import java.lang.System`. But if you don’t, the compiler adds this declaration automatically.

![](img/6d9dcff12e52b997f3ad31445b712549_381_0.png)

### The static `System.out` variable

What kind of importing must you do in order to abbreviate `System.out.println`? How can you shorten it to `out.println`? An import declaration lets you abbreviate a class’s name. But in the expression `System.out`, the word `out` isn’t a class. The word `out` is a static variable. (The `out` variable refers to the place where a Java program sends text output.) So you can’t write

```java
//This code is bogus. Don't use it:
import java.lang.System.out;
```

What do you do instead? You write

```java
import static java.lang.System.out;
```

To find out more about the `out` variable’s being a static variable, read the next section.

### All ye need to know

I can summarize much of Java’s complexity in only a few sentences.

- The Java API contains many packages.
- A package contains classes.
- From a class, you can create objects.
- An object can have its own methods. An object can also have its own variables.
- A class can have its own static methods. A class can also have its own static variables.

## Shedding light on the static darkness

I love to quote myself. When I quote my own words, I don't need written permission. I don't have to think about copyright infringement, and I never hear from lawyers. Best of all, I can change and distort anything I say. When I paraphrase my own ideas, I can't be misquoted.

With that in mind, here's a quote from the previous section:

> "Anything that's static belongs to a whole class, not to any particular instance of the class. . . To call a static method, you use a class's name along with a dot."

How profound! In Listing 18-6, I introduce a static method named parseInt. Here's the same quotation applied to the static parseInt method:

> The static parseInt method belongs to the whole Integer class, not to any particular instance of the Integer class. . . To call the static parseInt method, you use the Integer class's name along with a dot. You write something like Integer.parseInt(reply).

That's very nice! How about the System.out business that I introduce in Chapter 3? I can apply my quotation to that, too.

> The static out variable belongs to the whole System class, not to any particular instance of the System class. . . To refer to the static out variable, you use the System class's name along with a dot. You write something like System.out.println().

If you think about what System.out means, this static business makes sense. After all, the name System.out refers to the place where a Java program sends text output. (When you use Eclipse, the name System.out refers to Eclipse's Console view.) A typical program has only one place to send its text output. So a Java program has only one out variable. No matter how many objects you create — three, ten, or none — you have just one out variable. And when you make something static, you ensure that the program has only one of those things.

All right, then! The out variable is static.

To abbreviate the name of a static variable (or for a static method), you don't use an ordinary import declaration. Instead, you use a static import declaration. That's why, in Chapter 9 and beyond, I use the word static to import the out variable:

```java
import static java.lang.System.out;
```

## Barry makes good on an age-old promise

In Chapter 6, I pull a variable declaration outside of a main method. I go from code of the kind in Listing 18-9 to code of the kind that's in Listing 18-10.

**Listing 18-9: Declaring a Variable Inside the main Method**

```java
class SnitSoft {
    public static void main(String args[]) {
        double amount = 5.95;
        amount = amount + 25.00;
        System.out.println(amount);
    }
}
```

**Listing 18-10: Pulling a Variable Outside of the main Method**

```java
class SnitSoft {
    static double amount = 5.95;
    public static void main(String args[]) {
        amount = amount + 25.00;
        System.out.println(amount);
    }
}
```

In Chapter 6, I promise to explain why Listing 18-10 needs the extra word static (in static double amount = 5.95). Well, with all the fuss about static methods in this chapter, I can finally explain everything.

Refer to Figure 18-7. In that figure, you have checks, and you have a sort method. Each individual check has its own number, its own amount, and its own payee. But the entire Check class has just one sort method.

I don't know about you, but to sort my cancelled checks, I hang them on my exotic Yucca Elephantipes tree. I fasten the higher numbered checks to the upper leaves and put the lower numbered checks on the lower leaves. When I find a check whose number comes between two other checks, I select a free leaf (one that's between the upper and lower leaves).
