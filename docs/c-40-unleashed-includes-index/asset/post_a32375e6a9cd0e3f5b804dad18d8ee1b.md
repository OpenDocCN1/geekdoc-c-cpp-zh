
As an example of right-associativity, consider the following assignment:

```
a = b = c
```

Here, c will get evaluated first, after which it's assigned to b. The result of the assignment is then assigned to a. Yes, this means an assignment operation has a value, as you will see later:

```
a = (b = c)
```

## Evaluation of Subexpressions

Precedence and associativity define the order in which operators are applied to their operands. This is only part of the story, though. Another question is when the operands are turned into values that the operators can deal with. One of the reasons this is important is because of the potential side effects that occur during evaluation. Having a deterministic ordering for those is a welcome feature.

Let's set the scene by tweaking our preceding example just a tiny little bit:

```
int res = a() + b() * c();
```

Now a, b, and c are methods (or delegates, as discussed later) that get invoked. Ultimately, those return some value that's used for the operands of the various operators in this expression. Recall that the multiplication operator does bind stronger than the addition operator, so we already know the result of calling b and the result of calling c are going to feed in to the multiplication. We haven't said anything about the order in which these operands are evaluated, though.

To see why this matters, make a little transformation to the code, introducing temporary local variables for the evaluation results of the calls to a, b, and c:

```
int ta = a();
int tb = b();
int tc = c();

int res = ta + tb * tc;
```

From this, you can see that we've ordered the calls to a, b, and c in a left-to-right order. This is how the C# language specifies ordering for evaluation of subexpressions. Notice six orderings are possible in the preceding sample, but the left-to-right one is strictly enforced.

As mentioned before, this matters in the face of side effects. In this example, we've left those totally unspecified, but you could imagine a, b, and c printing something to the screen during evaluation. Thankfully, the order of those side effects is defined now.

## The Evaluation Stack

To get a feeling about the way code executes on the .NET platform and to be able to analyze fragments of intermediate language (IL) code, it's important to know the concept of the evaluation stack. IL is a stack-based language, meaning various operations pop their operands or arguments from the stack to carry out evaluation. When evaluation completes and a result is produced, it gets pushed on the stack.

To illustrate this, consider our running example again:

```
int a = 1;
int b = 2;
int c = 3;

int res = a + b * c;
```

To simplify matters, I'm using constant values for the three local variables. Everyone knows the result here is 7, so we could have hard-coded the value, but what matters to us is to see how the calculation is carried out.

You can guess the answer lies in ILDASM once more. Compile the preceding code into a simple console application and take a look at the resulting code. It should look like the one shown in Figure 5.2, assuming you've built in Debug mode.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_280_0.png)

FIGURE 5.2 Inspecting evaluation of expressions.

First, notice our four local variables are preserved and have the appropriate type. No surprise here. But let's take a closer look at the evaluation order.

## OPTIMIZATION?

Couldn't the compiler have optimized the preceding code to just the constant value 7? After all, none of the operands involved in the expression are known at compile time. Sure, in this case this would be completely safe to do (and in fact, some functional languages would), but in the general case, this is not safe.

The reason doesn't lie in the operands, but in the operators. As discussed later, operators can be overloaded so that custom types can define their own meaning for operators. If those operators do not behave as a pure function—that is, side effects can occur—it's not safe to change any of the runtime behavior.

In case of Int32 operands, it just happens the compiler can know all the behavior statically. But even that is a bit brittle in relation to arithmetic overflow behavior. We'll come back to that later in this chapter.

All in all, C# is an imperative language, and this kind of nontrivial compile-time evaluation is avoided. One exception is the use of literals: If you were to write 1 + 2 * 3 in your source code, it would get evaluated at compile time and substituted with an integer value 7.

The first couple of lines of IL are fairly straightforward; they just deal with assigning constant 32-bit integer values to our local variables a, b, and c:

```
IL_0000: nop
IL_0001: ldc.i4.1
IL_0002: stloc.0
IL_0003: ldc.i4.2
IL_0004: stloc.1
IL_0005: ldc.i4.3
IL_0006: stloc.2
```

However, we can already illustrate the essentials of the evaluation stack here. I've omitted the res variable from Figure 5.3, as well as the third assignment (for c).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_281_0.png)

FIGURE 5.3 Evaluation stack transitions for assigning constants to variables.

The nop instruction is simply a debug build artifact that corresponds to the opening curly brace in the code. This allows developers to set a breakpoint on that line. Following this, you'll see three pairs of ldc and stloc instructions. Those correspond to the assignment statements for a, b, and c. Their stack behavior is of particular interest:

- ldc loads a constant by pushing it onto the stack.
- stloc pops the top value from the stack and stores it in a local variable slot.

At the start of the method, the stack is empty. At the end of the method, it should be, too, to keep the evaluation stack balanced. Also observe how local variable slots are zeroed out upon entrance of the method.

So far, so good. You've seen how the constants get assigned to local variables. On to the evaluation of the expression now:

```
IL_0007: ldloc.0
IL_0008: ldloc.1
IL_0009: ldloc.2
IL_000a: mul
IL_000b: add
```

As you can guess, ldloc loads local variable slots and pushes the value onto the stack. The arithmetic instructions mul and add will pop two values from the stack, carry out the operation, and push the result, as shown in Figure 5.4.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_282_0.png)

FIGURE 5.4 Evaluation stack transitions for arithmetic operations.

## ABOUT REVERSE POLISH NOTATION AND HP CALCULATORS

Stack-driven evaluation as just described corresponds to postfix or reverse Polish notation, where the operator is written after its operands. For example, the infix a + b * c expression is turned into a b c * +. First a, b, and c are pushed on some stack, and then * reduces the top two values b and c by multiplying them, and finally + is performed over that result and a.

This approach has been very popular for use in desktop calculators (for example, the HP-10C series). With such calculators, you first enter operands (enter the digits, and then press Enter), and then carry out an operation (for example, by pressing +).

It's no coincidence that the CLR uses such a stack-based evaluation mechanism. Very machine-oriented in nature, it still provides enough abstraction over the way modern processors work. In reality—a reality that becomes true after Just-in-Time (JIT) compilation of IL code to x86 or x64 instructions—processors want operands in certain registers (like EAX and EBX) to carry out arithmetic operations on them. Similar arguments hold for calling conventions that use registers for efficiency. In IL, no affinity is taken to a particular machine architecture, thanks to the stack-based operation abstraction of the virtual machine.

Notice how the order of evaluation with regard to the *precedence* of the used arithmetic operators is respected. Finally, we’re left with the result of the evaluation on the stack (that is, the value 7) and are ready to assign it to the res variable:

```
IL_000c:  stloc.3
```

This puts our evaluation stack in an empty state again. The remaining instruction is a return. Although the containing method was declared as a procedure (void-returning, if you will), a ret instruction is required. This transfers control to the caller (in the case of the entry point, that’s the CLR infrastructure itself) to gracefully terminate the executing process.

```
IL_000d:  ret
```

## MANY STACKS

What we’ve talked about here is only the evaluation stack. IL instructions directly deal with this stack by pushing and popping values onto and from it. Think of it as a structured scratchpad.

Another stack is the call stack, which deals with maintaining (nested) method calls. Each method call has state associated with it in a so-called frame. This state includes things such as parameters, local variables used within the method, a return address, and space to return a value to the caller if desired. The call stack also serves a role in security enforcement with Code Access Security (CAS). During stack walks the call stack is used to make sure the right permissions are in place to make certain method calls.

In reality, those stacks are tightly related to one another, and together they make up the CLR stack. This should be considered just an implementation detail, though; it generally helps to think about both stacks separately because they serve different goals.
