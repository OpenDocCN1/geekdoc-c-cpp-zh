# Solutions to Chapter 10 | Mathematical

Q3 -> append x*3, x*5 and x*7 to Q3, Q5 and Q7. Remove x from Q3.
Q5 -> append x*5 and x*7 to Q5 and Q7. Remove x from Q5.
Q7 -> only append x*7 to Q7. Remove x from Q7.
Note: we do not need to append x*3 and x*5 to all lists because they will already be found in another list.

6. Repeat steps 4 - 6 until we've found k elements.

```
public static int getKthMagicNumber(int k) {
    if (k <= 0) return 0;
    int val = 1;
    Queue<Integer> Q3 = new LinkedList<Integer>();
    Queue<Integer> Q5 = new LinkedList<Integer>();
    Queue<Integer> Q7 = new LinkedList<Integer>();
    Q3.add(3);
    Q5.add(5);
    Q7.add(7);
    for (--k; k > 0; --k) // We've done one iteration already.
        val = Math.min(Q3.peek().intValue(),
            Math.min(Q5.peek().intValue(), Q7.peek().intValue()));
        if (val == Q3.peek()) {
            Q3.remove();
        } else
            if (val == Q5.peek()) {
                Q5.remove();
            } else { // must be from Q3
                Q3.remove();
            }
        Q3.add(val * 3);
        Q5.add(val * 5);
        Q7.add(val * 7);
    }
    return val;
}
```

# OBSERVATIONS AND SUGGESTIONS:

When you get this question, your best to solve it—even though it's really difficult. Explain a brute force approach (not as tricky) and start thinking about how you can optimize it. Try to find a pattern in the numbers.

Chances are, your interviewer will help you along when you get stuck. Whatever you do, don't give up! Think out loud, wonder aloud, explain your thought process. Your interviewer will probably jump in to guide you.