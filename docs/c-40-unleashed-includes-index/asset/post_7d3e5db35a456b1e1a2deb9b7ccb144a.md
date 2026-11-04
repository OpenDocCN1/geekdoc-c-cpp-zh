
```
}
public override string ToString()
{
    return string.Format("X = {0}, Y = {1}", _x, _y);
}
```

If Vector were to be defined as a class, the + operator obviously will simply accept null references. However, because the parameters on the + operator overload are not declared to be nullable, there's no way for those to receive null values. Instead, the language lifts the use of the + operator on nullable arguments:

```
Vector? v1 = new Vector(3, 4);
Vector? v2 = new Vector(2, 1);
Vector? v3 = null;

// Will print (5, 5). The type of v1 + v2 is by itself a Vector?.
Console.WriteLine(v1 + v2);

// All of those will simply print an empty line since the results are null.
Console.WriteLine(v1 + v3);
Console.WriteLine(v3 + v2);
Console.WriteLine(v3 + v3);
```

It's also possible for just one operand to be nullable. In that case, the non-nullable one will be converted to a nullable one, prior to invoking the operator.

To illustrate how the lifted + operator is implemented in terms of the non-lifted custom one, consider the following code:

```
static Vector? Add(Vector? v1, Vector? v2)
{
    return v1 + v2;
}
```

This code gets turned into the following equivalent piece of code. In reality, there are some slight differences, which are irrelevant to our discussion.

```
static Vector? Add(Vector? v1, Vector? v2)
{
    if (v1.HasValue && v2.HasValue)
        return v1.Value + v2.Value;  // Call our operator definition.
    return null;
}
```

## A Mandatory Listing

An exhaustive list of all the operators that can be overloaded is shown here. All but a few should look pretty straightforward. The others are the subject of further discussion in the following sections.

- Unary operators: +, -, ~, !, ++, --, true, false
- Binary operators: +, -, *, /, %, <<, >>, |, ^, <, <=, >, >=, ==, !=

Some operators are implemented in terms of the others. Examples include &&, ||, and the ternary conditional operator.

## Increment and Decrement, Pre and Post

The first two operators we take a look at are ++ and --. Because we all know from our discussion of expressions in Chapter 5, those operators can appear in two positions, as shown here. The result of running this code is that all variables will have a final value of 1.

```
int i = 0;

// j will be assigned i's value prior to incrementing it, hence it will be 0.
// After this post-increment, i's value will be equal to 1.
int j = i++;

// j will be pre-incremented before its updated value is used, and becomes 1.
// k gets this updated value of j, resulting in a value of 1.
int k = ++j;
```

When defining our own ++ (or --) operator, we can't control the behavior depending on the position in which the operator appears. For both uses, our operator's code will be called. All that's different is when this call happens. Another restriction on ++ and -- operators is that their return type should be the same as the defining type's or a subclass thereof. As an example, let's define a cursor class with a ++ operator on it. The definition of the class is trivial, containing one position field and an overload for ToString used for pretty printing. What's of more interest to us is the operator's definition:

```
public static Cursor operator ++(Cursor c)
{
    // The definition of Cursor is left as an exercise. A simple implementation
    // could just encapsulate an integer value. More advanced examples of a
    // cursor include a "caret" rendered in some custom textbox control, where
    // increment means moving the "caret" to the right.

    // Just return a new cursor that has advanced one position.
    // Contrast to C++'s overloading for this operator, one isn't asked to
    // change the incoming Cursor's position in place.
    return new Cursor(c._pos + 1);
}
```

With this in place, let's analyze how the operator gets invoked for the pre-increment and the post-increment uses of it. There should be no big surprises about this, and the output of the following code should be predictable:

```
var c = new Cursor(42);
Console.WriteLine("Before: " + c);
Console.WriteLine("During: " + c++);
Console.WriteLine("After: " + c);

var d = new Cursor(42);
Console.WriteLine("Before: " + d);
Console.WriteLine("During: " + ++d);
Console.WriteLine("After: " + d);
```

Got your solution ready? Here are the results. The first use, the post-increment one, will print 42 twice and 43 once. That is, the increment operator call for c happens after c's value has been used to compute the string concatenation that's put on the screen. For the second pre-increment example, the outcome is 42 once and 43 twice.

## Compound Assignment

The use of compound assignment (for example, +=) also supports user-defined operators. With a few simplifications around conversions and cases where complex expressions are used (requiring constituent expressions of the left side to be evaluated only once), the form a += b is turned into a = a + b. For the binary + operator, user-defined operators and lifted operators can be taken into consideration.

Reusing our vector example, the following fragment will use our operator definition:

```
Vector v1 = new Vector(3, 4);
Vector v2 = new Vector(2, 1);

// Turns into v1 = v1 + v2;
v1 += v2;

Console.WriteLine(v1);
```

Compound assignment can be used with all the overloadable binary operators that were listed before.

## Short-Circuiting Logical Operators and the Conditional Operator

Looking at the list of overloadable unary operators, two weird-looking operators catch the eye immediately. Aren't true and false just Boolean literals rather than operators? Obviously, the answer is no. The true and false unary operators play an important role in defining both of the short-circuiting && and || operators. It also helps out for the definition of the conditional operator.

To understand this, let's recap the behavior of those operators. What makes them so special? The short answer is that not all the expressions that are used as operands on the operator have to be evaluated in certain cases. Here is a code fragment that proves this point by means of side effects:

```
static bool PromptBool(string s)
{
    Console.Write(s);
    return bool.Parse(Console.ReadLine());
}

static int Get(string s)
{
    Console.WriteLine(s);
    return 42;
}

static void Main()
{
    bool and     = PromptBool("l: ") & PromptBool("r: ");
    Console.WriteLine("& -> " + and);

    bool andAlso = PromptBool("l: ") && PromptBool("r: ");
    Console.WriteLine("&& -> " + andAlso);

    bool or      = PromptBool("l: ") | PromptBool("r: ");
    Console.WriteLine("| -> " + or);

    bool orElse  = PromptBool("l: ") || PromptBool("r: ");
    Console.WriteLine("|| -> " + orElse);

    int res = PromptBool("condition: ") ? Get("true") : Get("false");
    Console.WriteLine("? : -> " + res);
}
```

By entering true or false at the prompts, you can easily illustrate the fact that some of the operators short-circuit evaluation as soon as the result can be determined.

For example, while the evaluation for and will always ask for a left and right operand value, the evaluation for andAlso won't. If the left operand value is false, there's no way the Boolean AND operation can still produce true. Because of this, the prompt for a right operand will never be displayed. A similar behavior exists for the Boolean OR operator's short-circuiting || variant: When the left operand evaluates to true, there's no point in evaluating the right operand anymore.

This is where the true and false operators come in. To define the short-circuiting && and || operators in terms of the & and | operators, the language specification says the following:

```
x && y  is evaluated as  T.false(x) ? x : T.&(x, y)
x || y  is evaluated as  T.true(x) ? x : T.|(x, y)
```

Because this is quite terse syntax, some further elaboration is most welcome. First, T here stands for the type defining the binary operator that got picked by resolution rules. In the syntax used for the language specification, calling an operator defined on a type simply looks like a static method invocation.

To evaluate a short-circuiting version of a binary logical operator, the first question the resulting code has to ask is whether the outcome of the operation can be determined by just looking at the first operand. This is precisely what true and false unary operators do. They ask this question: Hey, are you semantically equivalent to true (or false)? If that is not the case, the underlying binary operator is called.

### SYNTAX VERSUS SEMANTICS

The C# specification (like most other languages) quite intensively uses the English language to describe the semantics of various constructs. Although this works relatively well in practice, you must memorize lots of remarks to fully grasp some of the evaluation rules that are applied.

For example, in the excerpt for the definition of && and || in terms of &, |, true, and false shown earlier, there's a bit of imprecision because this literal transformation has different behavior than what's intended. Extra English-written clauses document that the expression for x will get evaluated only once and that this result will be reused for every appearance of x in the conditional operator.

In more-formal language specifications (of which I only know academic language examples), the semantics would shine through the (more mathematically dense) notation.

For example, with regard to overloading the binary logical & operator and enabling it for use in a short-circuited form, consider the following FilterBool struct. Such a type can come in handy for scenarios of scientific computing or bridging between C# code and some evaluation engine (like a database performing filter operations using Boolean logic):

```
struct FilterBool
{
    public static FilterBool operator &(FilterBool left, FilterBool right) {
        // Carry out the evaluation.
    }
}
```
