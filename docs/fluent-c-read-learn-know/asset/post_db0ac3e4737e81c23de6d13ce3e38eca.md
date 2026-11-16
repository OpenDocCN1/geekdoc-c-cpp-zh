

## ON YOUR OWN

Can you match the following terms to their definitions?

| Term | Definition |
|------|------------|
| Boolean Value | True or false. Sometimes called a “logical value”. |
| Operator | A symbol that acts on one or two values. |
| Increment Operator | An operator that adds 1 to the value of a variable and assigns the result to that variable. |
| Operand | A value that is evaluated by an operator. |
| Conditional Operator | A logical operator that doesn't evaluate the second operand if the first operand is sufficient to determine the result. |
| Boolean Expression | An expression that returns true or false. |

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_177_1.png)

## TAKE A BREAK

Boolean logic can seem really strange until you get the hang of it. The symbols look weird, and ‘x and ‘y’ doesn’t mean the same thing that it means in English. [If I ask you to give me all the clients in New York and California, I mean either, not both—a logical or, not an and.]

But why don’t you take a break before you move on to the Review? You might find you understand them better than you think you do.

## REVIEW

Circle the seven operators in the following statement. What type of value does the expression return?

```
x = ((y++ / 3) >= 15) && (--y < 5);
```

Given the declarations and initial values shown, re-write each of the following statements so that they return true instead of false:

```
Int32 x = 1;
Int32 y = 5;
Boolean a = true;
Boolean b = false;
```

- `x < x;`
- `(x <= x) ^ b;`
- `x > y;`
- `a & b;`
- `(x > y) | b;`

## OBJECT EXPRESSIONS

I’ve said (and it probably wasn’t news) that C# is an object-oriented language, and that objects are a programming construct that have STATE (things they know) and BEHAVIOR (things they do). You’ve seen that you create an object using a declaration statement, and that when you do, you must specify what type of object it is.

As we’ll see, you can define several different kinds of objects (called TYPES) in C#, but the one you’ll probably work with most often is the OBJECT. You already know how to create an instance of an object via a declaration statement. We’ll be looking at how to define objects beginning in Chapter 10. Right now, we’ll look at how you perform two important kinds of object expressions: member access, which gives you access to an object’s state, and method calls, which invoke its behavior.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_179_0.png)

## DOTS TO MEMBERS

So far, we've looked at literal expressions and operators that look (more or less) like the equations you remember from school. But there's a very important kind of expression that is hardly recognizable as one. It's called MEMBER ACCESS (the fields, properties, methods and events of a class are called its members), and the operator is a period ".", commonly referred to as the "dot operator".

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_180_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_180_1.png)

## METHOD SIGNATURES

You've already made some method calls, which simply means that you've gotten an object (in our examples, a MessageBox) to do something it knows how to do. We'll look at how to build methods starting in Chapter 8, but let's start now by exploring the SIGNATURE of a method, and what that means for how it's used.

This is the signature of a method. The signature is defined by the method name and the number and type of its parameters.

A PARAMETER specifies a value (either a literal value or a variable) that you pass to the method to work with. The method signature defines the type and name of each parameter.

Parameters are given names (conventionally in camelCase). The names are used to refer to the parameters within the method, but you don't need to use the same names for variables you use as ARGUMENTS (the values you pass to the method), and they aren't technically part of the signature.

Some methods return a value that can be assigned to a variable; their RETURN TYPE. If they don't, the return type is void.*

```
[Modifier] <ReturnType> <MethodName>(<type> <parameterName>, ...)
```

Modifiers determine where the method can be seen and how it can be modified. We'll examine them in Chapter 12.

Method names conventionally use PascalCase.

If a method needs more than one parameter, the parameters are separated by commas.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_181_0.png)

### WORDS FOR THE WISE

The data that's passed to a method and the code is called two different things, depending on the context. The abstract definition is a PARAMETER. But the actual values passed are ARGUMENTS. The distinction isn't critical, and people tend to use them interchangeably, but it is a valid difference: parameter is the description of the value, argument is the value itself.

## METHOD OVERLOADING

C#, and indeed all the .NET languages, allows you to define multiple methods with the same name, distinguished by their signatures. This process is called OVERLOADING, and the methods are called OVERLOADS. It saves you thinking up or remembering different method names for methods that vary only by their signature. Here's how the process works:

```
MessageBox.Show("message");
MessageBox.Show("message", "caption");
Window MyWindow = new Window();
MyWindow.Show();
```

Different classes can define methods with the same name. These aren't overloads—the simple fact that they belong to different classes distinguishes them.

The MessageBox.Show() overloads are distinguished by their signatures:

```
public static MessageBoxResult Show(string message);
public static MessageBoxResult Show(string message, string caption);
```

The return type (MessageBoxResult in this example) is not technically part of the signature, so you can't define two methods with the same name that are distinguished only by the values they return.

- It's really not a good idea to have overload with different return types anyway. It's too confusing.

The parameters are given the same name, but that isn't a requirement. Remember: the name isn't technically part of the signature; it's the type that distinguishes them.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_182_0.png)

## CALLING METHODS

When you put something like `MessageBox.Show("my message");` in your code, you’re technically doing something called INVOKING the method, but we commonly say that you’re CALLING the method, and the syntax is referred to as a METHOD CALL. You use the dot operator to call a method. (But you already knew that.)

You’ve used the Show() method of the MessageBox class several times now, and you’ve seen the support that IntelliSense gives for calling the method. Let’s have another look at that:

These numbers tell you how many overloads are defined for the method. In this example, you’re looking at the second of twelve.

This is the return type of the method. MessageBoxResult, another class. We’ve been ignoring it, which is always an option.

These are the parameters that define the signature for this version of the method.

▲ 2 of 12 ▼ MessageBoxResult MessageBox.Show(string messageBoxText, string caption)
Displays a message box that has a message and title bar caption; and that returns a result.
messageBoxText: A System.String that specifies the text to display.

Remember that the parameter names are used inside the method to refer to the values you’ve passed. You don’t have to use them when you call the method.

### UNDER THE MICROSCOPE

Symbolic operators like “+” and “/” are actually syntactic sugar. The compiler translates them into method calls like `Int32.Add(Int32 x, Int32 y).` You can always call the method directly, if it seems easier, or makes your intentions clearer. (But that doesn’t happen very often.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_184_0.png)

## HOW'D YOU DO?

Here's the signature of the Int32.Parse() method:

```
Int32 Parse(string s)
```

It takes a single parameter: a String that's given the name s.

The method returns an Int32.

The method name is Parse.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_184_1.png)

## UNDER THE MICROSCOPE—STATIC METHODS

Look at the example method calls on page 174 again. Do you notice something different about the way MessageBox.Show() and Window.Show() methods are called? MessageBox.Show() is called directly on the class itself, while Window.Show() is called on an instance of the method.

MessageBox.Show() is a STATIC METHOD. (Check out the signature—the method is declared with the static modifier.) We'll explore modifiers in detail in Chapter 12, but for right now, you should know that you don't need to instantiate a class in order to call a static method. You just specify the class name as though it were an instance, and pass whatever parameters are required.

Static methods are typically used for utility operations when all the information required to perform whatever the method does can be passed as parameters. (Static methods can't reference the object's state because there's no instance to store that information.)

The MessageBox.Show() method is pushing the limits of parameter passing. Some of the overloads require eight or nine parameters, and passing that many parameters quickly gets tedious. When you design your own classes, you'll need to think carefully about what's reasonable for your situation.

