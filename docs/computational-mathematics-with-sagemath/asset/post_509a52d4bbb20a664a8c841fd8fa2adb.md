
```python
sage: a, b = b, a
sage: a, b
(20, 10)
```

The assignment a, b = b, a is equivalent to swapping the values of a and b using an auxiliary variable:

```python
sage: temp = a; a = b; b = temp     # equivalent to: a, b = b, a
```

The following trick swaps the values of a and b without any auxiliary variable, using additions and subtractions:

```python
sage: x, y = var('x, y'); a = x ; b = y
sage: a, b
(x, y)
sage: a = a + b ; b = a - b ; a = a - b
sage: a, b
(y, x)
```

The instruction a = b = c = 0 assigns the same value, here 0, to several variables; the instructions x += 5 and n *= 2 are respectively equivalent to x = x+5 and n = n*2.

The comparison between two objects is performed by the double equal sign "==":

```python
sage: 2 + 2 == 2^2, 3 * 3 == 3^3
(True, False)
```

## 3.2 Algorithmics

The paradigm of *structured programming* consists in designing a computer program as a finite sequence of instructions, which are executed in order. Those instructions can be atomic or composed:

- an example of atomic instruction is the assignment of a value to a variable (cf. §1.2.4), or a result output;
- a composed instruction, like a loop or a conditional, is made up from several instructions, themselves atomic or composed.

### 3.2.1 Loops

**Enumeration Loops.** An enumeration loop performs the same computation for all integer values of an index *k* ∈ {*a*, . . . , *b*}: the following example³ outputs the beginning of the multiplication table by 7:

³When using Sage in a terminal, such a block of instructions must be ended by an additional empty line, which will be implicit in the whole book. This is not necessary when using Sage through a web browser.

```python
sage: for k in [1..5]:
....:     print(7*k)  # block containing a single instruction
7
14
21
28
35
```

The colon symbol “:” at the end of the first line starts the instruction block, which is evaluated for each successive value 1, 2, 3, 4 and 5 of the variable k. At each iteration, Sage outputs the product 7k via the print command.

In this example, the repeated instruction block contains a single instruction (namely print), which is indented to the right with respect to the for keyword. A block with several instructions has its instructions written one below the other, with the same indentation.

The block positioning is important: the two programs below, which differ in the indentation of a single line, yield different results.

```python
sage: S = 0
sage: for k in [1..3]:
....:     S = S+k
sage: S = 2*S
sage: S
```

```python
sage: S = 0
sage: for k in [1..3]:
....:     S = S+k
....:     S = 2*S
sage: S
```

On the left the instruction S = 2*S is executed only once at the end of the loop, while on the right it is executed at every iteration, which explains the different results:

$S=(0+1+2+3)\cdot 2=12\qquad S=((((0+1)\cdot 2)+2)\cdot 2+3)\cdot 2=22.$

This kind of loop will be useful to compute a given term of a recurrence, cf. the examples at the end of this section.

The syntax for k in [a..b] for an enumeration loop is the simplest one and can be used without any problem for 10⁴ or 10⁵ iterations; its drawback is that it explicitly constructs the list of all possible values of the loop variable before executing the iteration block, however it manipulates Sage integers of type Integer (see §5.3.1). Several .range functions allow iterations with two possible choices. The first choice is: either construct the list of possible values before starting the loop, or determine those values along with the loop iterations. The second choice is between Sage integers⁴ (Integer) and Python integers (int), those two integer types having slightly different properties. In case of doubt, the [a..b] form should be preferred.

⁴The commands srange, xrange and [...] also work on rational and floating-point numbers: try [pi,pi+5..20] for example.

**Iterations functions of the `.range` form for `a`, `b`, `c` integers**

|  |  |
|---|---|
| `for k in [a..b]: ...` | constructs the list of Sage integers a ≤ k ≤ b |
| `for k in srange(a, b): ...` | constructs the list of Sage integers a ≤ k < b |
| `for k in range(a, b): ...` | constructs a list of Python integers (int) |
| `for k in xrange(a, b): ...` | enumerates Python integers (int) without explicitly constructing the corresponding list |
| `for k in srange(a, b):` | enumerates Sage integers without constructing a list |
| `    [a..b, a..b, step=c]` | Sage integers a, a + c, a + 2c, ... as long as a + kc ≤ b |
| `    .range(b)` | equivalent to range(0, b) |
| `    .range(a, b, c)` | sets the iteration increment to c instead of 1 |

**TABLE 3.3 – The different enumeration loops.**

**While Loops.** The other kind of loops are the while loops. Like the enumeration loops, they execute a certain number of times the same sequence of instructions; however, here the number of repetitions is not known *a priori*, but depends on a condition.

The *while* loop, as its name says, executes instructions while a given condition is fulfilled. The following example computes the sum of the squares of non-negative integers whose exponential is less or equal to \(10^6\), i.e., \(1^2 + 2^2 + \cdots + 13^2\).

```python
sage: S = 0 ; k = 0        # The sum S starts to 0
sage: while e^k <= 10^6:   # e^13 <= 10^6 < e^14
....:     S = S + k^2      # accumulates the squares k^2
....:     k = k + 1
sage: S
819
```

The last instruction returns the value of the variable S and outputs the result:

\[
S = \sum_{\substack{k\in\mathbb{N}\\ e^k\le 10^6}} k^2 = \sum_{k=0}^{13} k^2 = 819,\qquad e^{13}\approx 442413 \le 10^6 < e^{14}\approx 1202604,
\]

The above instruction block contains two assignments: the first one accumulates the new term, and the second one moves to the next index. Those two instructions are indented in the same way inside the *while* loop structure.

The following example is another typical example of *while* loop. For a given number \(x \ge 1\), it seeks the unique integer \(n \in \mathbb{N}\) satisfying \(2^{n-1} \le x < 2^n\), i.e., the smallest integer with \(x < 2^n\). The program below compares \(x\) to \(2^n\), whose value is successively \(1, 2, 4, 8\), etc.; it performs this computation for \(x = 10^4\):

```python
sage: x = 10^4; u = 1; n = 0        # invariant: u = 2^n
sage: while u <= x: n = n+1; u = 2*u  # or n += 1; u *= 2
sage: n
14
```

As long as the condition \(2^n \le x\) is satisfied, this program computes the new values \(n+1\) and \(2^{n+1} = 2\cdot 2^n\) of the two variables \(n\) and \(u\), and stores them in place of \(n\) and \(2^n\). The loop ends when the condition is no longer fulfilled, i.e., when \(x < 2^n\):

$x = 10^4,\qquad \min\{n \in \mathbb{N} \mid x < 2^n\} = 14,\qquad 2^{13} = 8192,\qquad 2^{14} = 16384.$

Note that the body of a while loop is never executed when the condition is false at the first test.

As seen above, small command blocks can be typed on a single line after the colon “:”, without creating a new indented block starting at the next line.

**Aborting a loop execution**

The for and while loops repeat a given number of times the same instructions. The break command inside a loop interrupts it before its end, and the continue command goes directly to the next iteration. Those commands thus allow — among other things — to check the terminating condition at every place in the loop.

The four examples below determine the smallest positive integer $x$ satisfying $\log(x+1) \leq x/10$. The first program (top left) uses a for loop with at most 100 tries which terminates once the first solution is found; the second program (top right) looks for the smallest solution and might not terminate if the condition is never fulfilled; the third (bottom left) is equivalent to the first one with a more complex loop condition; finally the fourth (bottom right) has an unnecessarily complex loop structure, whose unique goal is to exhibit the continue command. In all cases the final value $x$ is 37.0.

```python
for x in [1.0..100.0]:
    if log(x+1)<=x/10:  break

x=1.0
while log(x+1)>x/10 and x<100:
    x=x+1
```

```python
x=1.0
while log(x+1)>x/10:
    x=x+1

x=1.0
while True:
    if log(x+1)>x/10:
        x=x+1
        continue
    break
```

The return command (which ends the execution of a function and defines its result, cf. §3.2.3) offers yet another way to abort early from an instruction block.

**Application to Sequences and Series**

The for loop enables us to easily compute a given term of a recurrent sequence. Consider for example the sequence $(u_n)$ defined by

$$u_0 = 1,\qquad \forall n \in \mathbb{N},\qquad u_{n+1} = \frac{1}{1+u_n^2}.$$

The following program yields a numerical approximation of $u_n$ for $n = 20$; the variable U is updated at each loop iteration to change from $u_{n-1}$ to $u_n$ according
