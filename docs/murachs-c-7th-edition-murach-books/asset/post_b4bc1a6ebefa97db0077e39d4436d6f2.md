
## Code that declares and uses variables with class scope

```
public frmInvoiceTotal()
{
    InitializeComponent();
}

decimal numberOfInvoices = 0m;
decimal totalOfInvoices = 0m;

private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal subtotal = Convert.ToDecimal(txtEnterSubtotal.Text);
    decimal discountPercent = .25m;
    decimal discountAmount = subtotal * discountPercent;
    decimal invoiceTotal = subtotal - discountAmount;

    numberOfInvoices++;
    totalOfInvoices += invoiceTotal;

    // the rest of the code for the method
}

private void btnClearTotals_Click(object sender, EventArgs e)
{
    numberOfInvoices = 0m;
    totalOfInvoices = 0m;
}
```

### Description

- The scope of a variable determines what code has access to it. If you try to refer to a variable outside of its scope, it will cause a build error.
- The scope of a variable is determined by where you declare it. If you declare a variable within a method, it has method scope. If you declare a variable within a class but not within a method, it has class scope.
- A variable with method scope can only be referred to by statements within that method. A variable with class scope can be referred to by all of the methods in the class.
- The lifetime of a variable is the period of time that it’s available for use. A variable with method scope is only available while the method is executing. A variable with class scope is available while the class is instantiated.
- You can declare class variables right after the code that is generated for a form.

## How to declare and use enumerations

An enumeration is a set of related constants that define a value type where each constant is known as a member of the enumeration. The enumerations provided by the .NET Framework are generally used to set object properties and to specify the values that are passed to methods. For example, the FormBorderStyle enumeration includes a group of constants that you can use to specify the settings for the FormBorderStyle property of a form.

The table in figure 4-16 summarizes three of the constants within the FormBorderStyle enumeration, and the first example shows how you can use code to set this form property. Normally, though, you’ll use the Properties window to choose the constant from the enumeration for this form property.

When writing code, you often need to select one option from a group of related options. For example, you may need to let a user choose the payment terms for an invoice. In that case, it often makes sense to define an enumeration that contains each option.

To define an enumeration, you can use the syntax shown in this figure. After you provide a name for an enumeration, you code the constant names within braces. In the first example, the enumeration is named Terms, and the constants are named Net30Days, Net60Days, and Net90Days. In this case, because values aren’t provided for these constants, the default values of 0, 1, and 2 are assigned to the constants.

If you want to assign other values to the constants, you can provide a value for each constant as shown in the second example. Here, the values 30, 60, and 90 are assigned to the constants for the TermValues enumeration. In this case, these values are stored as short data types because a colon and the data type are coded after the enumeration name. If the data type is omitted, the constant values are stored as integers.

To refer to a constant value in an enumeration, you code the name of the enumeration followed by a dot and the name of the constant. This is illustrated by the first three statements in the third group of examples. Here, the first statement returns a value of the Terms type, the second statement returns the int type that corresponds to a member of the Terms enumeration, and the third statement returns the int type that corresponds to a member of the TermValues enumeration. If you want to refer to the name of a constant instead of its value, you can use the ToString() method as in the last example in this group.

For now, when you code an enumeration, you can code it with class scope. In other words, you can code the enumeration after the generated code for a class as shown in the previous figure. That way, it will be available to all of the methods in the class. Later, when you learn how to add classes to a project, you can store an enumeration in its own file so it’s easily accessible from all classes in the project.

### Some of the constants in the FormBorderStyle enumeration

| Constant | Description |
|---|---|
| FormBorderStyle.FixedDialog | A fixed, thick border typically used for dialog boxes. |
| FormBorderStyle.FixedSingle | A single-line border that isn’t resizable. |
| FormBorderStyle.Sizable | A resizable border. |

### A statement that uses the FormBorderStyle enumeration

```
this.FormBorderStyle = FormBorderStyle.FixedSingle;
```

### The syntax for declaring an enumeration

```
enum EnumerationName [: type]
{
    ConstantName1 [= value][,
    ConstantName2 [= value]]...
}
```

### An enumeration that sets the constant values to 0, 1, and 2

```
enum Terms
{
    Net30Days,
    Net60Days,
    Net90Days
}
```

### An enumeration that sets the constant values to 30, 60, and 90

```
enum TermValues : short
{
    Net30Days = 30,
    Net60Days = 60,
    Net90Days = 90
}
```

### Statements that use the constants in these enumerations

```
Terms t = Terms.Net30Days;
int i = (int) Terms.Net30Days;          // i is 0
int i = (int) TermValues.Net60Days;     // i is 60
string s = Terms.Net30Days.ToString();  // s is "Net30Days"
```

### Description

- An *enumeration* defines a set of related constants. Each constant is known as a *member* of the enumeration.
- By default, an enumeration uses the int type and sets the first constant to 0, the second to 1, and so on.
- To use one of the other integer data types, you can code a colon after the enumeration name followed by the data type.
- To specify other values for the constants, you can code an equal sign after the constant name followed by the integer value.

## How to work with nullable value types and the null-coalescing operators

By default, value types (such as the int, decimal, and bool types) can’t store null values. By contrast, reference types (such as the string type) can store null values by default. Most of the time, you won’t need to use a value type to store null values. However, a feature of C# known as nullable types allows you to store a null value in a value type, and figure 4-17 shows how this feature works.

To declare a nullable value type, you type a question mark (?) immediately after the type in the declaration of a value type. Except for the question mark, this works just as it does for any other value type variable. In this figure, for example, the first statement declares an int variable as a nullable type. Then, the second statement uses the null keyword to assign a null value to this type.

Typically, you use a null value to indicate that the value of the variable is unknown. For example, if a user didn’t enter a quantity, you might want to assign a null value to the quantity variable to indicate that the user didn’t enter a value. When working with value types, however, it’s more common to assign a default value such as zero to indicate that the user didn’t enter a value. As a result, unless you’re working with a database that returns null values, you probably won’t need to use nullable value types.

In addition to the built-in value types, this figure shows that you can declare the Terms enumeration shown in figure 4-16 as a nullable type. That makes sense because enumerations define value types.

Once you declare a value type as nullable, you can use the HasValue property to check if the type stores a value or if it contains a null value. Then, if it stores a value, you can use the Value property to get that value. In the next chapter, you’ll learn how to use an if statement to test the value of the HasValue property of a nullable type to determine if the type is null. Then, you can execute different sets of statements depending on the result.

Another way to test the value of a nullable type is to use the null-coalescing operator. This operator returns the value of the left operand—in this case, the nullable type—if it isn’t null. Otherwise, it returns the value of the right operand. This operator makes it easy to assign a default value to a variable if a nullable type contains null. In the statement in this figure, for example, a value of -1 will be assigned to the variable named qty if the nullable type named quantity is null.

Sometimes, you only want to assign a value to a variable if that variable is null. To do that, you can use the null-coalescing assignment operator. In this figure, for example, a value of 0.0 will be assigned only if salesTotal is null.

Note that you can use the null-coalescing operators with reference types as well as nullable value types, since reference types can be null by default. Note, however, that C# 8.0 introduced a compiler option that you can use to make reference types non-nullable by default. If you turn this compiler option on, you have to explicitly declare reference types as nullable. You’ll learn more about how this works in chapter 9.

You can also use nullable value types in arithmetic expressions. In that case, if the value of the nullable type is null, the result of the arithmetic expression is always null. This is illustrated in the last example in this figure.
