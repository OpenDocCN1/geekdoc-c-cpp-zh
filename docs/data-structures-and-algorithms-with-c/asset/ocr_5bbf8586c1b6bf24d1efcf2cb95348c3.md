We can call this as x^n to the power of n" or "x raised to the power of n". Here, x is the base and n is the exponent or the power.

Now, x^n can be defined recursively as follow:

x^n = \begin{cases} 1, & \text{if } n = 0 \\ x \cdot x^{n-1}, & \text{Otherwise} \end{cases}

# Function to find out power using recursion

```
FUNCTION: INT POWER (X, N)
[ X is the base and N is the exponent]
1. [Base Condition]
   If N=0 then Return 1
2. [Check whether negative exponent]
   Else If N<0 then Call Power(X, N+1)/X
3. Else call Power (X, N-1)*X
   [End of If]
4. Return
```

Power by the squaring method can minimize the number of multiplications. Power by the squaring method can be defined on recursively as follows:

x^n = \begin{cases} x.(x^{(n-1)/2})^2, & \text{if n is odd} \\ (x^{n/2})^2, & \text{if n is even} \end{cases}

When n is an even number then
x^n = x^(2z) = (x^z)^2, where n = 2z,
When n is an odd number then
x^n = x^(2z+1) = x * (x^z)^2 where n = 2z+1.

# Function to find out power using recursion

```
FUNCTION: INT POWER (X, N)
1. If N=0 then Return 1
2. If N<0 then Call Power(1/X, -N)
3. Set P = 1
4. If N mod 2 = 1 then P = X
5. P = P * Power (X*X, N/2)
6. Return P
```

By using this method, we can minimize the multiplication operations. This algorithm uses [log2 n] squares and at most [log2 n] multiplications. For instance, when n=15, the above algorithm required 3 squares and 3 multiplications, 6 multiplications in total. However, it does not always do the fewest possible number of multiplications.