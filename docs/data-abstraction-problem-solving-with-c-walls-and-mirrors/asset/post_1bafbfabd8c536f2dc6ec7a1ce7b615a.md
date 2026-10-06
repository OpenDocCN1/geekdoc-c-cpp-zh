
# Organizing Data

As the position of a person was generally known to be a soft job, there were many applicants. Scholars and peasants alike brought the emperor their solutions. Many solutions were thousands of steps long, and many contained deeply nested loops and control structures. "I can't understand these solutions," bellowed the emperor. "There must be an easy way to solve this puzzle."

And there was a Great Buddhist monk came out of the mountains to see the emperor. "My son," he said, "the puzzle is easy, almost solves itself." The emperor's security chief wanted to throw this strange person out, but the emperor let him come.

"If you have only one disk (that is, $n=1$), move it from pole A to pole B." So far, so good, but even the village idiot could get that right. "If you have more than one disk (that is, $n>1$), simply

- 1. Ignore the bottom disk and the small modification that pole C is the destination and pole B is the source. (See Figure 2-16b).
- 2. After you have done this, $n-1$ disks will be on pole C, and the largest disk will remain on pole A. Solve the problem for n (I recall that even the village idiot could do this) by moving the large disk from A to B. (See Figure 2-16c).
- 3. Now you have to move the $n-1$ disks from pole C to pole B; that is, solve the problem with pole C as the source, pole B as the destination, and pole A as the source. (See Figure 2-16d).

There was silence for a moments, and finally the emperor said impatiently, "Well, are you going to tell us your solution or not?" The monk gave an all-knowing smile and vanished.

The emperor was obviously not a recursive thinker, but you should realize that you can solve the monk's solution by solving three times the number of disks—Towers. Let us count (count, source, destination, spare) define the problem of moving disks from pole source to destination using pole as spare. Notice that this method makes sense if there are more than count disks on pole source; in this case, concern yourself with only the top disks and ignore the others. Similarly, the destination and source have disks on them before you move them; ignore these too, except that you may place only smaller disks on top of them.

You can restate the emperor's problem as follows: Beginning with $n$ disks on pole A and zero disks on poles B and C, solve towers $(n, A, B, C)$. You can solve the monk's solution as follows:

**Step 1.** Starting in the initial state—with all the disks on pole A—solve the problem towers $(n-1, A, C, B)$. That is, ignore the bottom (largest) disk and move the top $n-1$ disks from pole A to pole C, using pole B as spare. When you are finished, the largest disk will remain on pole A, and all the other disks will be on pole C.

**Step 2.** Now, with the largest disk on pole A and all other disks on pole C, solve the problem towers $(1, A, B, C)$. That is, move the largest disk from pole A to pole B. This disk is larger than the disks already on pole C, you could not use the spare. However, fortunately—and obviously—you do not need to use the spare in this case. When you are done, the largest disk will be on pole B, and all other disks remain on pole C.

**Step 3.** Finally, with the largest disk on pole B and all the other disks on pole C, solve the problem towers $(n-1, C, B, A)$. That is, move the $n-1$ disks from pole C to pole B, using pole A as spare. Notice that the destination pole B already has the largest, which you ignore. When you are done, you will have solved the original problem: All the disks will be on pole B.

The problem statement
The solution

## CHAPTER 2 Recursion: The Mirrors

The problem towers(count, source, destination, spare) has the following pseudocode solution:

```
solveTowers(count, source, destination, spare)
if (count is 1)
    Move a disk directly from source to destination
else
    solveTowers(count - 1, source, spare, destination)
    solveTowers(1, source, destination, spare)
    solveTowers(count - 1, spare, destination, source)
```

This recursive solution follows the same pattern as the recursive solutions you saw earlier in this chapter:

- 1. You solve Towers by solving other Towers.
- 2. These other Towers are smaller than the original problem; they have fewer disks to move. In particular, the number of disks decreases by 1 each recursive call.
- 3. When a problem has only one disk—the base case—the solution is easy.
- 4. That the problem smaller ensures you will reach base case.

Solving the problem requires you to solve smaller recursively. Figure 2-17 illustrates the recursive calls and order when you solve the problem for three disks. Now consider a C++ implementation of this algorithm. Since most computers do not have arms (at the time of writing), the function moves a disk by giving directions to human. Thus, the parameters that represent poles are of type char, and arguments could be 'A', 'B', and 'C'. The call solveTowers(3, 'A', 'B', 'C') produces this output:

```
Move disk from pole A to B
Move disk from pole A to C
Move disk from pole B to C
Move disk from pole A to B
Move disk from pole C to A
Move disk from pole A to B
```

The order of recursive calls that results from solveTowers(3, A, B, C) is FIGURE 2-17. The solution to Towers problem satisfies four criteria of recursive solution for three disks: img/d0cb862f18b2db56996ad7c743510e4_0.png

The C++ function follows:

```cpp
void solveTowers(int count, char source, char destination, char spare) {
    if (count == 1) {
        cout << "Move disk from pole " << destination << endl;
    }
    else {
        solveTowers(count - 1, source, spare, destination); // X
        solveTowers(1, source, destination, spare); // Y
        solveTowers(count - 1, spare, destination, source); // Z
    }
} // end solveTowers

Trace execution of function solveTowers to solve Towers problem for two disks.

One possible solution is to define rabbit(0) to be 0, which seems artificial. A slightly more attractive alternative is to treat rabbit(2) itself as a special case with the value of 1. Thus, the recursive definition has two cases, rabbit(2) and rabbit(1). The recurrence definition is:

```
rabbit(n) = { 1 if n < 2 else rabbit(n - 1) + rabbit(n - 2) }
```

The series of rabbit(1), rabbit(2), and rabbit(3), is also known as the Fibonacci sequence, models many naturally occurring phenomena. rabbit computes the Fibonacci sequence but so inefficiently.

## 2.6 More Examples

The next three problems require you to count certain events or combinations of things. They are good examples of recursive solutions with base case. However, these solutions are tremendously inefficient and not practical. Do not let this inefficiency discourage you. Recursion can be useful even though it is not always so. Your goal right now is to understand recursion by examining simple problems.

Rabbitits are prolific breeders. If rabbits did not breed, their population would quickly get out of hand. Suppose we assume the following facts, which were obtained in a recent survey of randomly selected:

- Rabbits never die.
- Rabbits reach maturity exactly two months after birth; at the beginning of its third month of life.
- Rabbits are always born in female-pairs. At the beginning of every month, each female-pair gives birth to exactly one female-pair.

Suppose that started with a single newborn female-pair. How many pairs would there be in month 6? As it is a relatively small number, you can figure out the solution:

- Month 1: 1 pair, the original rabbits.
- Month 2: 1 pair still, because rabbits are not yet mature.
- Month 3: 2 pairs; the original pair has reached maturity and has given birth to a second pair.
- Month 4: 3 pairs; the original pair has given birth again, but the pair born at the beginning of month 3 are not yet mature.
- Month 5: 5 pairs; all alive in month 3 (2 pairs) are now mature. Add their offspring to those alive in month 4 (3 pairs) to yield 5 pairs.
- Month 6: 8 pairs; 3 newborn pairs from pairs alive in month 4 plus 5 pairs alive in month 5.

## 2.6.1 The Fibonacci Sequence (Multiplying Rabbits)

You can now construct a recursive solution for rabbit(n), the number of pairs alive in month n. You must determine how you use rabbit(n - 1) to compute rabbit(n). Observe that rabbit(n) is the sum of the number of pairs just prior to the start of month n and the number of pairs alive in month n born at the start of n. Just prior to the start of month n, there are rabbit(n-1) pairs of rabbits. Not all of these rabbits are mature at the start of month n. Only those that were alive in n-2 are ready to produce at the start of month n. Thus, if the number of pairs born at the start of month n is rabbit(n-2), you have the recurrence relation the number of pairs in month n:

```
rabbit(n) = rabbit(n - 1) + rabbit(n - 2)
```

Figure 2-18 illustrates this relationship.

Figure 2-18 Recursive solution to the rabbit problem: img/d0cb862f18b2db56996ad7c743510e106_0.png

This recurrence relation—like some previous examples—solves a problem by solving more than one smaller problem of the same type. This does not add much conceptual difficulty, but you must be careful when selecting the base case. The temptation is to say that rabbit(1) should be the base case because its value is 1 according to the problem's statement. But what about rabbit(2)? Applying the recurrence definition to rabbit(2) would yield:

```
rabbit(2) = rabbit(1) + rabbit(0)
```

Thus, the recursive definition would need to specify the number of pairs alive in month 0—under-defined quantity.
