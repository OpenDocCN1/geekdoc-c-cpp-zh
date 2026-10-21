programs is not the languages—Java versus Python—but the features being used—imperative versus functional. The programming language features used in the imperative variant (assignment statements, loops) and in the functional variant (higher-order functions, lambda expressions) exist independently from Java and Python; indeed, they are available in many programming languages.

I am not saying that programming languages don't matter. We all know that, for a given task, some languages are a better fit than others. But I want to emphasize core features and concepts that extend across languages, even when they appear under a different syntax. For instance, an experienced Python programmer is more likely to write the example functional program in this way:

```
def rand_shift(nums, rand):
    return [shifted for shifted in (num + rand.randrange(-10, 11) for num in nums)
        if shifted > 0]
```

This code looks different from the earlier Python code—and the details are again unimportant. Notice that functions map and filter are nowhere to be seen. Conceptually, though, this is the same program but written using a specific Python syntax known as list comprehension, instead of map and filter.

The important concept to understand here is the use of map and filter (and more generally higher-order functions, of which they are an example), not list comprehension. You benefit from this understanding in two ways. First, more languages support higher-order functions than have a comprehension syntax. If you are programming in Java, for instance, you will have to write map and filter explicitly (at least for now). Second, if you ever face a language that uses a somewhat unusual syntax, as Python does with list comprehension, it will be easier to recognize what is going on once you realize that it is just a variation of a concept you already understand.

The preceding code examples illustrate a contrast between a program written in plain imperative style and one that leverages the functional programming features available in many languages. I can make a similar argument with concurrent programming. Languages (and libraries) have evolved, and there is no reason to write today's concurrent programs the way we did 20 years ago. As a somewhat extreme example, travel back not quite 20 years to 2004, the days of Java 1.4, and consider the following problem:

> Given two tasks that each produce a string, invoke both tasks in parallel and return the first string that is produced.

Assume a type StringComputation with a string-producing method compute. In Java 1.4, the problem can be solved as follows (do not try to understand the code; it is rather long, and the details are unimportant):