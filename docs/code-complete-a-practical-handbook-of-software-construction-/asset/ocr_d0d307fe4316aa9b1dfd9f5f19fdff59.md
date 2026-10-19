true by definition. If the changes didn’t degrade the internal structure, we wouldn’t consider them to be optimizations; we would use them by default and consider them to be standard coding practice.

Cross-Reference Code tunings are heuristics. For more on heuristics, see Section 5.3, “Design Building Blocks: Heuristics.”

Some books present code-tuning techniques as “rules of thumb” or cite research that suggests that a specific tuning will produce the desired effect. As you’ll soon see, the “rules of thumb” concept applies poorly to code tuning. The only reliable rule of thumb is to measure the effect of each tuning in your environment. Thus, this chapter presents a catalog of “things to try,” many of which won’t work in your environment but some of which will work very well indeed.

# 26.1 Logic

Cross-Reference For other details on using statement logic, see Chapters 14–19.

Much of programming consists of manipulating logic. This section describes how to manipulate logical expressions to your advantage.

# Stop Testing When You Know the Answer

Suppose you have a statement like

```
if ( 5 < x ) and ( x < 10 ) then ...
```

Once you’ve determined that x is greater than 5, you don’t need to perform the second half of the test.

Cross-Reference For more on short-circuit evaluation, see “Knowing How Boolean Expressions Are Evaluated” in Section 19.1.

Some languages provide a form of expression evaluation known as “short-circuit evaluation,” which means that the compiler generates code that automatically stops testing as soon as it knows the answer. Short-circuit evaluation is part of C++’s standard operators and Java’s “conditional” operators.

If your language doesn’t support short-circuit evaluation natively, you have to avoid using and and or, adding logic instead. With short-circuit evaluation, the code above changes to this:

```
if ( 5 < x ) then
    if ( x < 10 ) then ...
```

The principle of not testing after you know the answer is a good one for many other kinds of cases as well. A search loop is a common case. If you’re scanning an array of input numbers for a negative value and you simply need to know whether a negative value is present, one approach is to check every value, setting a negativeFound variable when you find one. Here’s how the search loop would look: