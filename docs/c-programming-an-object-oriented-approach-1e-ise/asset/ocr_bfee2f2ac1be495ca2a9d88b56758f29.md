# **Program 17.5** Using the recursive isPalindrome function (Continued)

```
```cpp
27  if (strg.size() <= 1)
28  {
29      return true;
30  }
31  else if (strg[0] != strg[strg.size() - 1])
32  {
33      return false;
34  }
35  return isPalindrome (strg.substr (1, strg.size() - 2));
36  }

Run:
Is "a palindrome? true    // empty string
Is 'rotor' a palindrome? true
Is 'hello' a palindrome? false
```
```

# ### 17.1.3 Tail and Nontail Recursive Functions

We encountered two types of recursion in the examples that we discussed in the previous sections: *tail recursion* and *nontail recursion* (Figure 17.8).

# Tail Recursion

In **tail recursion**, each general case terminates after calling the next general case or the base case. In other words, the duty of the general case is just to call the next general function or the base function. The duty of the base case is to return the result of the whole operation to the *main* function. In tail recursion, the stack that holds the record of the next function call has only one record because when the next function is called, the current function terminates.

![](bbox=[0.251, 0.632, 0.829, 0.858])

**Figure 17.8** Difference between a tail and a nontail function