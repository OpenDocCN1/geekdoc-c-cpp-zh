
```c
using static System.Console;
delegate void GreetHandler(string s);
class Greeting {
    public static void Hello(string s)
    {
        WriteLine("Hello, {0}", s);
    }
    public static void Goodbye(string s)
    {
        WriteLine("Goodbye, {0}", s);
    }
    static void Main()
    {
        GreetingHandler firstDel, secondDel;
        firstDel = new GreetHandler(Hello);
        secondDel = new GreetHandler(Goodbye);
        GreetMethod(firstDel, "Cathy");
        GreetMethod(secondDel, "Bob");
    }
    public static void GreetMethod(GreetingHandler gd,
        string name)
    {
        WriteLine("The greeting is:");
        gd(name);
    }
}
```

Figure 13-6 The greeting program

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_630_0.png)

Figure 13-7 Output of the greeting program

Delegates are useful in that method reference can be passed to another method, so the receiving method can be customized. With many other features of C# (and all other programming languages), you can use other techniques to accomplish the same result. For example, you can gladly produce simple output as Hello, Cathy using other techniques. However, you are learning a little about delegates here because, you will see later in this chapter, they are used in the code that responds to events in C#'s GUI environment.

## Creating Composed Delegates

You can assign one delegate to another using the = operator. You can also use the + and -= operators to combine delegates into a composed delegate that calls the delegates from which it is built. As an example, assume that you have delegates named del11, del12, and del13, and that you assign a reference to the method M1() to del11 and a reference to method M2() to del12. When the statement del13 = del11 + del12 executes, it becomes a delegate that executes both M1() and M2(), in order. Only delegates with the same parameter list can be combined, and the delegates must have a void return type. Additionally, you can use the - -= operators to remove a delegate from a composed delegate. A composed delegate is a collection of delegates, and the += and -= operators add and remove items from the collection.

Figure 13-8 shows a program that contains a composed delegate. This program contains two changes from the Greet program in Figure 13-6: the class name (Greeting2) and the shaded statement that creates the composed delegate. The delegate firstDel now executes two methods, Hello() and Goodbye(), whereas secondDel still executes Goodbye().
Figure 13-9 shows its output: Cathy is used with two methods, Bob is used with only one.

```c
using static System.Console;
delegate void Greeting(string s);
class Greeting2
{
    public static void Hello(string s)
    {
        WriteLine("Hello, {0}!", s);
    }
    public static void Goodbye(string s)
    {
        WriteLine("Goodbye, {0}!", s);
    }
    public static void Main()
    {
        GreetingHandler firstDel = new GreetingHandler(Hello);
        secondDel = new GreetingHandler(Goodbye);
        firstDel += secondDel;
        GreetMethod(firstDel, "Cathy");
        GreetMethod(secondDel, "Bob");
    }
    public static void GreetMethod(GreetingHandler gd, string name)
    {
        WriteLine("The greeting is:{0}");
        gd(name);
    }
}
```

**Figure 13-8** The Greeting2 program

## CHAPTER 13 Handling Events

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_632_0.png)

**Figure 13-9** Output of the Greeting2 program

Watch the video *Event Handling*.

## TWO TRUTHS & A LIE
Understanding Delegates

- 1. A delegate is an object that contains a reference to a method.
- 2. Once you have created a delegate, it can encapsulate any method with the same identifier as the delegate.
- 3. A composed delegate can be created using the += operator; it calls the delegates from which it is built.

> The false statement is #2. Once you have created a delegate, the return type and parameter list must match that of the delegate. It can encapsulate.

## You Do It

Creating Delegates
To demonstrate how delegates work, you create two delegate instances in the next steps and assign different method references to them.

- 1. Open a new console project named **DiscountDelegateDemo**. Type the necessary code using statements, and then create a delegate that encapsulates a void method that accepts a double argument:

```c
using System;
using System.Console;
delegate void DiscountHandler(ref double saleAmount);
(continues)
```

- 2. Begin creating a DiscountDelegateDemo class that contains a StandardDiscount() method. The method accepts a reference parameter that represents an amount of a sale. If the sale amount is at least $1,000, a discount of 5 percent is calculated and subtracted from the sale amount. If the sale amount is not least $1,000, nothing is subtracted.

```c
class DiscountDelegateDemo {
    public static void StandardDiscount(ref double saleAmount) {
        const double DISCOUNT_RATE = 0.05;
        const double CUTOFF = 1000.00;
        double discount;
        if(saleAmount >= CUTOFF) {
            saleAmount *= DISCOUNT_RATE;
        } else {
            discount = 0;
            saleAmount -= discount;
        }
    }
```

- 3. Add a PreferredDiscount() method. The method also accepts a reference parameter that represents the amount of a sale and calculates a discount of 10 percent on every sale.

```c
public static void PreferredDiscount(ref double saleAmount) {
    const double SPECIAL_DISCOUNT = 0.10;
    double discount = saleAmount * SPECIAL_DISCOUNT;
    saleAmount -= discount;
}
```

- 4. Add a Main() method that declares variables whose values (a sale amount and a code) will be supplied by the user. Declare two DiscountHandler objects named firstDel and secondDel. Assign a reference to the StandardDiscount() method to oneHandler and a reference to the PreferredDiscount() method to the other.

```c
static void Main() {
    double saleAmount;
    char code;
    DiscountHandler firstDel, secondDel;
    firstDel = new DiscountHandler(StandardDiscount);
    secondDel = new DiscountHandler(PreferredDiscount);
}
```

- 5. Continue the Main() method with prompts to the user to enter a sale amount and a code. Then, depending on the code, use the appropriate delegate to calculate the correct value for saleAmount. Display the value and add closing braces for the Main() method and the class.

```c
Write("Enter amount of sale ");
saleAmount = Convert.ToDouble(ReadLine());
Write("S for standard discount, " +
  "P for preferred discount");
code = Convert.ToChar(ReadLine());
if(code == 'S')
    firstDel(ref saleAmount);
else
    secondDel(ref saleAmount);
WriteLine("New sale amount is {0}", saleAmount.ToString("C2"));
```

- 6. Save the file, and then compile and execute it. Figure 13-10 shows the results when the program is executed several times.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_634_0.png)

**Figure 13-10** Sample executions of the DiscountDelegate- program

When you compose delegates, you can invoke multiple method calls using a single statement. In the next steps, you create a composed delegate to demonstrate how composition works.

- Open the DiscountDelegateDemo file, and immediately save it as DiscountDelegateDemo.
- Within the Main() method, add a third Delegate object to the statement that declares the two existing versions, as follows:
DiscountHandler firstDel, secondDel, thirdDel;
- After the statements that assign values to the existing Delegate objects, add statements that assign the firstDel object to thirdDel, and then add secondDel to it composition.
thirdDel = firstDel;
thirdDel += secondDel;
- Change the prompt for the code, as follows, to reflect three options. The standard and preferred discounts remain the same, but the extreme discount (supposed for special customers) provides both types of discounts, first subtracting 5 percent for any sale equal to or greater than $1,000, and then providing a discount of 10 percent more.
- Change the if statement so that if the user does not enter S or P, then the extreme discount applies.

```csharp
Write("Enter S for standard discount, " + 
  "P for preferred discount," + 
  "\nX for extreme discount\");
```

```csharp
if(code == 'S')
  firstDel(ref saleAmount);
else
  if(code == 'P')
    secondDel(ref saleAmount);
else
  thirdDel(ref saleAmount);
```
