
Now look at a parsing tree as we used above for expressions, but used here for simple English:

## **Parsing a simple English sentence**

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_226_0.png)

This is not all that complicated. If you had trouble with §6.4, then please go back and read it from the beginning; it may make more sense the second time through!

### 6.4.2 Writing a grammar

How did we pick those expression grammar rules? “Experience” is the honest answer. The way we do it is simply the way people usually write expression grammars. However, writing a simple grammar is pretty straightforward: we need to know how to

1. Distinguish a rule from a token
2. Put one rule after another (*sequencing*)
3. Express alternative patterns (*alternation*)
4. Express a repeating pattern (*repetition*)
5. Recognize the grammar rule to start with

Different textbooks and different parser systems use different notational conventions and different terminology. For example, some call tokens _terminals_ and rules _non-terminals_ or _productions_. We simply put tokens in (double) quotes and start with the first rule. Alternatives are put on separate lines. For example:

```
List:
     "{" Sequence "}"
Sequence:
    Element
    Element " ," Sequence
Element:
    "A"
    "B"
```

So a **Sequence** is either an **Element** or an **Element** followed by a **Sequence** using a comma for separation. An **Element** is either the letter **A** or the letter **B**. A **List** is a **Sequence** in “curly brackets.” We can generate these **Lists** (how?):

```
{ A }
{ B }
{ A,B }
{A,A,A,A,B }
```

However, these are not **Lists** (why not?):

```
{ }
A
{ A,A,A,A,B
{A,A,C,A,B }
{ A B C }
{A,A,A,A,B, }
```

This sequence rule is not one you learned in kindergarten or have hardwired into your brain, but it is still not rocket science. See §7.4 and §7.8.1 for examples of how we work with a grammar to express syntactic ideas.

### 6.5 Turning a grammar into code

There are many ways of getting a computer to follow a grammar. We’ll use the simplest one: we simply write one function for each grammar rule and use our type **Token** to represent tokens. A program that implements a grammar is often called a _parser_.

#### 6.5.1 Implementing grammar rules

To implement our calculator, we need four functions: one to read tokens plus one for each rule in our grammar:

```
get_token()
	// read characters and compose tokens
	// uses cin
expression()
	// deal with + and -
	// calls term() and get_token()
term()
	// deal with *, /, and %
	// calls primary() and get_token()
primary()
	// deal with numbers and parentheses
	// calls expression() and get_token()
```

Note: Each function deals with a specific part of an expression and leaves everything else to other functions; this radically simplifies each function. This is much like a group of humans dealing with problems by letting each person handle problems in his or her own specialty, handing all other problems over to colleagues.

What should these functions actually do? Each function should call other grammar functions according to the grammar rule it is implementing and get_token() where a token is required in a rule. For example, when primary() tries to follow the (Expression) rule, it must call

```
get_token()
	// to deal with ( and )
expression()
	// to deal with Expression
```

What should such parsing functions return? How about the answer we really wanted? For example, for 2+3, expression() could return 5. After all, the information is all there. That’s what we’ll try! Doing so will save us from answering one of the hardest questions from our list: “How do I represent 45+5/7 as data so that I can evaluate it?” Instead of storing a representation of 45+5/7 in memory, we simply evaluate it as we read it from input. This little idea is really a major breakthrough! It will keep the program at a quarter of the size it would have been had we had expression() return something complicated for later evaluation. We just saved ourselves about 80% of the work.

The “odd man out” is get_token(): because it deals with tokens, not expressions, it can’t return the value of a sub-expression. For example, + and ( are not expressions. So, it must return a Token. We conclude that we want

```
// functions to match the grammar rules:
Token get_token()
	double expression()
	// read characters and compose tokens
	// deal with + and -
double term()    // deal with *, /, and %
double primary()    // deal with numbers and parentheses
```

#### 6.5.2 Expressions

Let’s first write **expression()**. The grammar looks like this:

```
Expression:
  Term
  Expression '+' Term
  Expression '-' Term
```

Since this is our first attempt to turn a set of grammar rules into code, we’ll proceed through a couple of false starts. That’s the way it usually goes with new techniques, and we learn useful things along the way. In particular, a novice programmer can learn a lot from looking at the dramatically different behavior of similar pieces of code. Reading code is a useful skill to cultivate.

##### 6.5.2.1 Expressions: first try

Looking at the **Expression '+' Term** rule, we try first calling **expression()**, then looking for **+** (and **−**) and then **term()**:

```
double expression()
{
  double left = expression();  // read and evaluate an Expression
  Token t = get_token();       // get the next token
  switch (t.kind) {            // see which kind of token it is
  case '+':
    return left + term();      // read and evaluate a Term,
                               // then do an add
  case '-':
    return left − term();      // read and evaluate a Term,
                               // then do a subtraction
  default:
    return left;               // return the value of the Expression
  }
}
```

It looks good. It is almost a trivial transcription of the grammar. It is quite simple, really: first read an **Expression** and then see if it is followed by a **+** or a **−**, and if it is, read the **Term**.

Unfortunately, that doesn't really make sense. How do we know where the expression ends so that we can look for a **+** or a **-**? Remember, our program reads left to right and can't peek ahead to see if a **+** is coming. In fact, this **expression()** will never get beyond its first line: **expression()** starts by calling **expression()** which starts by calling **expression()** and so on “forever.” This is called an *infinite recursion* and will in fact terminate after a short while when the computer runs out of memory to hold the “never-ending” sequence of calls of **expression()**. The term *recursion* is used to describe what happens when a function calls itself. Not all Recursions are infinite, and recursion is a very useful programming technique (see §8.5.8).

##### 6.5.2.2 Expressions: second try

So what do we do? Every **Term** is an **Expression**, but not every **Expression** is a **Term**; that is, we could start looking for a **Term** and look for a full **Expression** only if we found a **+** or a **-**. For example:

```
double expression()
{
    double left = term();                 // read and evaluate a Term
    Token t = get_token();                 // get the next token
    switch (t.kind) {                      // see which kind of token that is
    case '+':
        return left + expression();        // read and evaluate an Expression,
                                            // then do an add
    case '-':
        return left – expression();        // read and evaluate an Expression,
                                            // then do a subtraction
    default:
        return left;                       // return the value of the Term
    }
}
```

This actually – more or less – works. We have tried it in the finished program and it parses every correct expression we throw at it (and no illegal ones). It even correctly evaluates most expressions. For example, **1+2** is read as a **Term** (with the value **1** followed by **+** followed by an **Expression** (which happens to be a **Term** with the value **2**) and gives the answer **3**. Similarly, **1+2+3** gives **6**. We could go on for quite a long time about what works, but to make a long story short: How about **1–2–3**? This **expression()** will read the **1** as a **Term**, then proceed to read **2–3** as an **Expression** (consisting of the **Term 2** followed by the **Expression 3**). It will then subtract the value of **2–3** from **1**. In other words, it will evaluate **1–(2–3)**. The value of **1–(2–3)** is **2** (positive two). However, we were taught (in primary school or even earlier) that **1–2–3** means **(1–2)–3** and therefore has the value **–4** (negative four).
