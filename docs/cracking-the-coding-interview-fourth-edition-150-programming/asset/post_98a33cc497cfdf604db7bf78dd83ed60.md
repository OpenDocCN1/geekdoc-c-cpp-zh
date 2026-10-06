
# At the Interview | Handling Technical Questions

- Question: And are the numbers integers?
- Answer: Yes.
- Question: Where did the numbers come from? Are they IDs? Values of something?
- Answer: They are the ages of customers.
- Question: And how many customers are there?
- Answer: About a million.

We now have a pretty different problem: sort an array containing a million integers between 0 and 130. How do we solve this? Just create an array with 130 elements and count the number of ages at each value.

# Step 2: Design an Algorithm

Designing an algorithm can be tough, but our five approaches to algorithms can help you see out (pg 34). While you're designing your algorithm, don't forget to think about:

- What are the space and time complexities?
- What happens if there is a lot of data?
- Does your design cause other issues? (i.e., if you're creating a modified version of a binary search tree, will your design impact the time for insert / delete)?
- If there are other issues, did you make the trade-offs?
- If they give you specific data (e.g., mentioned that the data is ages, or in sorted order), have you leveraged that information? There's probably a reason that you're given it.

# Step 3: Pseudo-Code

Writing pseudo-code can help you outline your thoughts clearly and reduce the number of mistakes you commit. But make sure to tell your interviewer you're writing pseudocode first and that you'll follow it up with "real". Many candidates will write pseudocode in order to 'escape' writing code, and you certainly don't want to be confused with those candidates.

# Step 4: Code

You don't need to rush through your code; in fact, this will most likely hurt you. Just go at a nice, slow methodical pace. Also, remember this advice:

- Use Data Structures Generously: Where relevant, use a good data structure or define your own. If you're asked a problem involving finding the minimum age for a group of people, consider defining a data structure to represent a Person. This shows your interviewer you care about good object oriented design.
- Don't Crowd Your Coding: This is a minor thing, but it can really help. When you're writing code on a whiteboard, start in the upper left hand corner - not in the middle. This will give you plenty of space to write your answer.

# Step 5: Test

Yes, you need to test your code! Consider testing for:

- Extreme cases: 0, negative, null, maximums, etc
- User error: What happens if the user passes in null or a negative value?
- General cases: Test the normal case.

If the algorithm is complicated or highly numerical (bit shifting, arithmetic, etc.), consider testing while you're writing the code rather than just at the end.

Also, when you find mistakes (which you will), carefully think through why the bug is occurring. One of the worst things I saw while interviewing candidates who recognized a mistake and tried making "random" changes to fix the error.

For example, imagine a candidate writes a function that returns a number. When he tests his code with the number '5' he notices that it returns 0 when it should be returning 1. So, he changes the last line from "return ans" to "return ans+1," without thinking through why this would resolve the issue. Not only does this look bad, but it also sends the candidate on an endless string of bugs and bug fixes.

When you notice problems in your code, really think deeply about why your code failed before fixing the mistake.

# At the Interview | Five Algorithm Approaches

# Five Algorithm Approaches

There's no sure approach to solving a tricky algorithm problem, but the approaches below can be useful. Keep in mind that the more problems you practice, the easier it will be to identify which approach to use.

Also, remember that the five approaches can be “mixed and matched.” That is, once you’ve applied “Simplify & Generalize”, you may want to implement Pattern Matching next.

# APPROACH I: EXAMPLING

Description: Write out specific examples of the problem, and see if you can figure out a general rule.

Example: Given a time, calculate the angle between the hour and minute hands.

Approach: Start with an example like 3:27. We can draw a picture of a clock by selecting where the 3 hour hand is and where the 27 minute hand is.

By playing around with these examples, we can develop a rule:

- Minute angle (from 12 o'clock): 360 minutes / 60
- Hour angle (from 12 o'clock): 360 * (hour % 12) / 12 + 360 * (minutes / 60) * (1 / 12)
- Angle between hour and minute: hour angle - minute angle % 60

By simple arithmetic, this reduces to 30 * hours - 5.5 * minutes.

# APPROACH II: PATTERN MATCHING

Description: Consider what problems the algorithm is similar to, and figure out if you can modify the solution to develop an algorithm for this problem.

Example: A sorted array has been rotated so that the elements might appear in the order 3 4 5 6 7 1 2. How would you find the minimum element?

Similar Problems:

- Find the minimum element in an array.
- Find a particular element in an array.

Algorithm: Finding the minimum element in an array isn't particularly interesting. However, if the array is rotated and we want to find the minimum element in an array (you could iterate through all the elements), binary search is very applicable. You know that the array is sorted, but rotated. This means the range is still increasing.

![](img/50974dc108b2978cf2cacf9397df99.png)

# APPROACH III: SIMPLIFY & GENERALIZE

Description: Change a constraint (data type, size, etc) to simplify the problem. Then try to solve it. Once you have an algorithm for the "simplified" problem, generalize the problem again.

Example: A random note can be formed by cutting words out of a magazine to form a new sentence. How would you figure out if a ransom note (string) can be formed from a given magazine (string)?

Simplification: Instead of solving the problem with words, solve it with characters. That is, imagine we are cutting characters out of a magazine to form a ransom note.

Algorithm: We can solve the simplified ransom note problem with characters by simply creating an array and counting characters. Each spot in the array corresponds to one letter. First, we count the number of times each character in the ransom note appears, and then we go through the magazine to see if we have all of those characters.

When we generalize the algorithm, we do a very similar thing. This time, rather than creating an array with character counts, we create a hash table. Each word maps to the number of times the word appears.

# APPROACH IV: BASE CASE AND BUILD

Description: Solve the algorithm for a base case (e.g., just one element). Then, try to solve it for elements one and two, assuming that you have the answer for element one. Then, try to solve it for elements one, two and three, assuming that you have the answer elements one and two.

Example: Design an algorithm to print all permutations of a string. For simplicity, assume all characters are unique.

```
Test String: "abcdef"
Case "a" --> {a}
Case "ab" --> {ab, ba}
Case "abc" --> ?
```

This is the first "interesting" case. If we had the answer to P("ab"), how could we generate P("abc"). Well, the additional letter is "c", so we can just stick c in every possible point.
