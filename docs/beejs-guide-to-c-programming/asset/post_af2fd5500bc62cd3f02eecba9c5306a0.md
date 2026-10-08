
Other folks online point out that there's no way to detect a VLA's failure to allocate, and programs that suffered such problems would likely just crash. While fixed-size arrays also have the same issue, it's far more likely that someone accidentally make a VLA Of Unusual Size than somehow accidentally declare a fixed-size, say, 30 megabyte array.

# Chapter 31

# goto

The goto statement is universally revered and can be here presented without contest.

Just kidding! Over the years, there has been a lot of back-and-forth whether or not (often not) to goto is considered harmful¹.

In this programmer's opinion, you should use whichever constructs leads to the best code, factoring in maintainability and some times this might be goto!

In this chapter, we'll see how goto works in C, and then check out some of the common cases where it is used².

## 31.1 A Simple Example

In this example, we're going to use goto to skip a line of code and jump to a label. The label is the identifier that can be a goto target—it ends with a colon (:).

```c
#include <stdio.h>

int main(void)
{
    printf("One\n");
    printf("Two\n");

    goto skip_3;

    printf("Three\n");

skip_3:
    printf("Five\n");
}
```

The output is:

One
Two
Five!

> ¹https://en.wikipedia.org/wiki/Goto#Criticism

> ²I'd like to point out that using goto in all these cases is avoidable. You can use variables and loops instead. It's just that some people think goto produces the best code in those circumstances.

# Chapter 31. goto

goto sends execution jumping to the specified label, skipping everything in between.

You can jump forward or backward with goto.

```c
infinite_loop:
    print("Hello, world!\n");
    goto infinite_loop;
```

Labels are skipped over execution. The following will print all three numbers in order just as if the labels weren't there:

```c
printf("Zero\n");
label_1:
    printf("One\n");
label_2:
    printf("Two\n");
label_3:
    printf("Three\n");
```

As you've noticed, it's a common convention to justify all the labels on the left. This increases readability because a reader can quickly scan to find the destination.

Labels have function scope. That is, no matter how many levels in blocks they appear, you can still get them from anywhere in the function.

It means you can only go labels that are in the same function as the goto itself. Labels in other functions are out of goto's perspective. And it means you can use the same label name in two functions—just not the same label in the same function.

## 31.2 Labeled continue

In languages, you can actually specify a label for a continue statement. C doesn't allow it, but you can easily use goto instead.

To show the issue, check out continue in this nested loop:

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d, %d\n", i, j);
        continue; // Always goes to next
    }
}
```

As we see, continue, like all continues, goes to the next iteration of the nearest enclosing loop. If we want to continue in the next loop out, right?

Well, we can break to get to the outer loop, right?

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d, %d\n", i, j);
        break; // Gets us to the next iteration of
    }
}
```

That gets us levels of nested loop. If we nest another loop, we're out of options. What about this, where we don't have any statement that will get us to the next iteration of i?

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        for (int k = 0; k < 3; k++) {
            printf("%d, %d, %d\n", i, j, k);
        }
        continue; // Gets us to the next iteration of k
        break; // Gets us to the next iteration of j
        ????; // Gets us to the next iteration of i???
    }
}
```

The goto statement offers us a way!

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        for (int k = 0; k < 3; k++) {
            printf("%d, %d, %d\n", i, j, k);
        }
        goto continue_i; // Now continuing the i loop!
    }
    continue_i;
}
```

We have at the end here—that's because you can't have a label pointing to the plain end of a compound statement (or before a variable declaration).

## 31.3 Bailing Out

When you're super nested in the middle of code, you can use goto to get out of it in a manner that's often cleaner than nesting more ifs and using flag variables.

```c
// Pseudocode
for(...) {
    for (...) {
        while (...) {
            do {
                if (some_error_condition)
                    goto bail;
            } while(...);
        }
    }
}

bail:
// Cleanup here
```

Without goto, you'd have to check an error condition flag in all of the loops to get all the way out.

## 31.4 Labeled break

This is a very similar situation to how continue only the innermost loop. break also only breaks out of the innermost loop.

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d, %d\n", 1, j);
        break; // Only breaks out of the j loop
    }
}

printf("Done!\n");
```

But we can goto to break further:

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d, %d\n", 1, j);
        goto break_i; // Now breaking out of the i loop
    }
}

break_i:
printf("Done!\n");
```

## 31.5 Multi-level Cleanup

If you're calling multiple functions to initialize multiple systems and one of them fails, you should only de-initialize the ones that you've got to far.

Let's do a fake example where we start initializing systems and checking to see if any returns an error (we'll use -1 to indicate an error). If one of them does, we have to shutdown down the systems we've initialized so far.

```c
if (init_system_1() == -1)
    goto shutdown;

if (init_system_2() == -1)
    goto shutdown_1;

if (init_system_3() == -1)
    goto shutdown_2;

// Success!
shutdown_2:
shutdown_1:
// Cleanup system 2
shutdown:
// Cleanup system 1
```

## 31.6 Tail Call Optimization

(Note: The text provided in the OCR seems to be fragmented or repetitive in this section, but based on the context of Tail Call Optimization and the provided code snippets):

The goto statement offers us a way to implement tail call optimization manually. A tail call is when the last action of a function is to return another function call. By using goto to jump back to the start of the function, we can avoid adding a new stack frame.

