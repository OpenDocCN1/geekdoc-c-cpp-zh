```
    30            {
    31                B[ i ] = B[ j ];
    32                i ++;
    33            }
    34        }
    35        if (ntemp % 2 == 0) ntemp = (ntemp / 2);
    36        else if (res[i] == 0) ntemp = floor(ntemp / 2);
    37        else ntemp = ceil(ntemp / 2);
    38    }
    39    for(i = 0; i < n; i ++)
    40    std::cout << res[i];
    41 }
    42 }
    43 }
```

We claim the algorithm implemented by this program solves correctly the problem of determining the missing bit. First we prove it is correct.

# Proving the Correctness of the program

Define that a complete array of size n is a two dimensional bit array similar to the above A but without any missing column from it. Clearly, such an array has n + 1 columns. For instance, a complete array of size 10 would be the following:

![](bbox=[0.23, 0.535, 0.79, 0.625])

Define that an almost complete array of size n is a two dimensional bit array with precisely one missing column from it. It follows the array A in the current problem is an almost complete array of size n. Now consider any complete array Ā of size n. Call L̄ the bottom row of Ā. That L̄ consists of the least significant bits of the numbers from Ā. Let n̄₀ be the number of zeros and n̄₁, the number of ones, in L̄. Let Δ̄ = n̄₀ − n̄₁. We claim that:

Δ̄ = { 0, if n is odd; 1, if n is even.  (2.3)

Indeed, it is trivial to prove by induction that if the number n + 1 of columns in Ā is even then Δ̄ = 0 and if it is odd, Δ = 1.

Now consider A: any almost complete array of size n, obtained from Ā by deleting a column, i.e., the missing number. Let L be the bottom