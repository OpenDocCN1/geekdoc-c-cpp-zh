
## ON YOUR OWN

Why don't you try using the Debug constant, just to get a sense for how directives work?

Add the code on the previous page to the chapter project, and run it to make sure that "Debug is defined" is displayed in the MessageBox.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_158_0.png)

Change the Define DEBUG constant checkbox and re-run the application to make sure that "Debug isn't defined" is displayed.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_158_1.png)

## DEFINING DIRECTIVES

The Project Properties Designer provides an easy way to control the definition of the two most common constants used with directives: DEBUG and TRACE. But you can also use the #define directive to define these constants or create ones of your own.

```
#define MYCONST
```

Directive constants aren't case-sensitive, but it's customary to use all caps so that they stand out.

The #define directive does exactly what you'd expect: It defines a directive constant.

```
#undef MYCONST
```

The #undef directive is the opposite of #define: it un-defines the constant. This is useful if you want a constant defined while one part of the code is executing, but not in some other part.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_159_0.png)

## ON YOUR OWN

Try adding #define MYCONST and #undef MYCONST to your Project so that both MessageBox statements execute.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_159_1.png)

## TAKE A BREAK

You're almost finished with the first pure language chapter. Was it what you expected? Why don't you take a break now, before we complete the review, and then we'll move on to expressions?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_160_0.png)

## REVIEW

Write a single statement that declares an Int32 and sets its initial value to 200:

Re-write the declaration as three separate statements:

- Which of the following are legal identifiers in C#?
  - myIdentifier
  - 12Things
  - Some Elephant
  - #Items

What are the three types of comments recognized by the C# compiler, and how do you begin each one?

What character do you use to begin a directive?

## Congratulations! You've finished the chapter. Take a minute to think about what you've accomplished before you move on to the next one...

List three things you learned in this chapter:

- 1
- 2
- 3

Why do you think you need to know these things in order to be a C# programmer?

Is there anything in this chapter that you think you need to understand in more detail? If so, what are you going to do about that?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_162_0.png)

## C# LANGUAGE, PART 2: TRANSITIVE VERBS

In the last chapter you saw how to create the nouns of C#, declared elements. In this chapter, we'll look at one of the two kinds of verbs: the EXPRESSIONS that are roughly (very roughly!) equivalent to transitive verbs. (If it's been a while since you studied grammar, a transitive verb is one that takes both a subject and an object: "He bought the book.")

Many people equate programming expressions to mathematical formulae. That's not wrong, exactly, but expressions are a lot more than that. Of course you can say, "x = 1 + 1" in C#, and you'll use an expression to say it, but you'll also use expressions to say things like, "If Dumbo is an elephant, give him some peanuts" and, "Greedy wants the biggest apple in the barrel."

By the way, programming doesn't require nearly as much mathematics as some people think. In fact, unless you're writing a mathematical application or doing certain kinds of graphics work, it requires hardly any at all. And the computer will do all the arithmetic for you. Personally, I find that comforting.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_164_0.png)

## C# LANGUAGE ELEMENTS

We're continuing our study of the C# parts of speech in this chapter.

### LANGUAGE ELEMENTS

We explored comments and directives in the last chapter.

- COMMENTS
- DIRECTIVES
- STATEMENTS
  - Expressions are a kind of statement.
- EXPRESSIONS
  - Expressions are the subject of this chapter.
- COMMANDS
  - We'll look at commands in the next chapter.
- DECLARATIONS
  - We studied declarations in the last chapter, too.

## IN A NUTSHELL

## EXPRESSIONS

We'll explore method calls in Chapter 8.

### METHODS

```
MessageBox.Show();
```

LINQ expressions are primarily used for data handling, things like "show me all the vegetable providers who sell artichokes."

We won't be studying LINQ in this book.

### LITERAL

```
a = x + 1;
```

### SPECIAL

### IDENTIFIERS

```
myIdentifier
```

Yes, names like myIdentifier really are considered expressions in C#, because the compiler has to do something to resolve a name. There really isn't anything more for us to learn about these.

### LINQ

```
from e in myColl
select e;
```

### LAMBDAS

```
(x, y) => x * y
```

A lambda is an anonymous expression, roughly equivalent to using var to declare an anonymous variable. We'll see an example of lambda expressions when we study WPF binding in Chapter 22.

## TASK LIST

In the last chapter, we examined comments, directives, and one kind of C# statement: the declaration statements that create the nouns you'll work with. In this chapter, we'll look at one of the two remaining types of statements: expressions.

## BASIC EXPRESSIONS

What in spoken English is generally called an "equation", in C# is called a literal expression. In addition to basic arithmetic, C# literal expressions include text manipulation (combining strings, for example) and an important category of logical formulas called Boolean expressions. We'll look at all of these in this chapter.

## OBJECT EXPRESSIONS

C# is an object-oriented language, which means that it models what the application needs to do as a set of programming constructs (technically called types, of which objects are one kind) that have state (they know things) and behavior (they can do things). We'll be looking at exactly what this means and how to do it throughout the rest of the book, and we'll get started here by looking at how to get at the behavior exposed by .NET types: by calling methods.

## MAKE A NOTE

You're going to run into a lot of new concepts in this chapter, and I won't be explaining all of them right away. (It's a problem; just about every aspect of programming is related to just about every other aspect.)

Don't panic. You don't need to understand everything about everything right away. Just concentrate on figuring out how expressions work, and the other bits will fall into place in a chapter or two.

Like transitive verbs in spoken English, a C# expression performs some action on some thing. In English, the action is called the "verb", and the thing it acts on is the "object". In C#, the equivalent of the verb is the OPERATOR, and the object is the OPERAND. These are the same terms used in mathematics, but C# expressions don't often look like mathematics (unless, of course, you're actually doing mathematics). Let's look at some examples:

This is probably the kind of thing you think of when you hear the word "equation", and by extension, "C# expression":

```
a = 1 + 2
```

But C# expressions can do a lot more. This isn't a mathematical equation, but it is a valid C# expression:

```
TextBox.Text = "Hello, world";
```

The equals sign is the operator. It's called the ASSIGNMENT OPERATOR, and you'll use it all the time. Roughly translated, it means "take whatever's to the right of me, and put the result in whatever's to the left of me."

In C#, operands don't always operate on numbers. Here's another example:

```
TextBox.Text = "Hello, " + "world";
```

The plus sign here is the CONCATENATION OPERATOR, that combines strings. We'll look at it in detail in Chapter 10.

## EXPRESSIONS VS. EQUATIONS

Many C# expressions look just like mathematical equations. They have an operand on either side of an operator, and the operators look like the ones you used for arithmetic. But it's important to keep sight of the fact that C# expressions are NOT mathematical equations.

### Expressions don't always have two operands, although they always have at least one:

-1
You probably don't think of this as an expression, but it is NEGATION. The operator is the minus sign.

x++
This is the POST-INCREMENT operator. It adds 1 to the value of x, and we'll be seeing more of it later.

x? y : z
This strange looking syntax is the conditional operator. It returns y if x is true, or z if x is false. We'll be examining it in more detail in the next chapter.

### Operators don't always look like mathematical symbols. Some of them are words, and the most important of these, new, you've already used:

new Elephant()
This probably looks familiar by now.

true
true looks like a value, and the truth is it usually behaves like a value, too. But because it's actually an operator, you can re-define the meaning of true and false when you start building your own classes (which we'll do in Chapter 8).

### Operands aren't always numeric values, even when the operators look like arithmetic:

"Hello, " + "World!"
The operands here are, of course, strings of characters, not numbers. The plus sign, in this situation called the CONCATENATION OPERATOR, sticks the string to its right at the end of the string to its left: "Hello, World!" We'll examine strings and how to manipulate them in detail in Chapter 10.
