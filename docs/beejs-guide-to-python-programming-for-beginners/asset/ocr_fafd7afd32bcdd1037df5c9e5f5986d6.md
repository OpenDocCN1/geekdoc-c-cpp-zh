*Blocks can be indented with any combination of tabs or spaces, as long as each line in the block begins with the same pattern of tabs or spaces. The official recommendation is to use 4 spaces for indentation in Python.*

*Indented blocks in Python are one of the things most devs are pretty opinionated about in terms of loving or hating. Personally, I say be a good dev in any language, regardless of how you feel about their idiosyncrasies.*

And then what's this pesky else? That's a super-handy feature of if. If the condition is False, then the block under the else is evaluated instead. Basically, we're saying, "If the condition is true, then do this, otherwise do this."

There's one more construct we can use in the if-else family: elif. This is short for else if and is used if you need to check multiple conditions.

```
if x < 10:
    print("x is less than 10")
elif x < 20:
    print("x is less than 20")
elif x < 30:
    print("x is less than 30")
else:
    print("x is greater than or equal to 30")
```

In that example, first we check if x is less than 10. If that's False, the next condition is tested, and so on. If none of them match, then we get to the else case.

The if statement is the core of what allows us to use Boolean logic to control the flow of our program. It's how computers can make decisions based on input. Without if, there would be no computing—that's how important it is!

And your job as a dev is to come up with that logic, those if statements and conditions, that cause your program to give the proper output for a given input.

# 6.7 And Now: while Loops!

Problem-solving step: Understanding the Problem.

We're going to divert ever-so-slightly, and talk about another important concept in programming: loops. A loop is what allows us to execute the same piece of code repeatedly without repeating ourselves.

Here's a real-life example. Let's say you have to add some shingles to a roof. The steps to do so are to place a shingle, nail it in place, and then move to the next spot.

Instructions for four shingles might be:

+   - Place a shingle
+   - Nail it on
+   - Move to the next spot
+   - Place a shingle
+   - Nail it on
+   - Move to the next spot
+   - Place a shingle
+   - Nail it on
+   - Move to the next spot
+   - Place a shingle
+   - Nail it on
+   - Move to the next spot

But that's irksomely verbose. It would be nicer to do something like this:

+   - While we haven't yet placed 4 shingles:
+     - Place a shingle
+     - Nail it on