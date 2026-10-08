tests! So, we must choose tests and to choose, we need some principles for making a choice:

+   - Test for *likely mistakes* (find the most errors).
- Test for *bad mistakes* (find the errors with the worst potential consequences).

By “bad,” we mean errors that would have the direct consequences. In general, that’s a fuzzy notion, but it can be made precise for a specific program. For example, for a binary search considered in isolation, all errors are about equally bad, but if we used that **binary_search()** in a program where all answers were carefully double-checked, getting a wrong answer from **binary_search()** might be far more acceptable than having it not return because it went into an infinite loop. In that case, we would spend greater effort tricking **binary_search()** into an infinite (or very long) loop than we would trying to trick it into giving a wrong answer. Note our use of “tricking” here. Testing is – among other things – an exercise in applying creative thinking to the problem of “How can we get this code to misbehave?” The best testers are not just systematic, but also quite devious (in a good cause, of course).

# 26.3.2.1 Testing strategy

How do we go about breaking **binary_search()**? We start by looking at **binary_search()**‘s requirements, that is, what it assumes about its inputs. Unfortunately, from our perspective as testers, it is clearly stated that **[first,last)** must be a sorted sequence; that is, it is the caller’s job to ensure that, so we can’t fairly try to break **binary_search()** by giving it unsorted input or a **[first,last)** where last<first. Note that the requirements for **binary_search()** do not say what it will do if we give it input that doesn’t meet its requirements. Elsewhere in the standard, it says that it may throw an exception in that case, but it is not required to. These facts are good to remember for when we test uses of **binary_search()**, though, because a caller failing to establish the requirements of a function, such as **binary_search()**, is a likely source of errors.

We can imagine the following kinds of errors for **binary_search()**:

+   - Never returned (e.g., infinite loop)
- Crash (e.g., bad reference, infinite recursion)
- Value not found even though it was in the sequence
- Value found even though it wasn’t in the sequence

In addition, we remember the following “opportunities” for user errors:

+   - The sequence is not sorted (e.g., ⟨2,1,5,−7,2,10⟩).
- The sequence is not a valid sequence (e.g., **binary_search(&a[100], &a[50],77)**).