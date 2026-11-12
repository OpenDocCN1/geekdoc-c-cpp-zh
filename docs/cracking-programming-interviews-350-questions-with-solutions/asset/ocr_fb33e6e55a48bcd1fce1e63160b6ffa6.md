![](bbox=[0.24, 0.06, 0.76, 0.17])

Consider positions 7 = 2^{\lfloor \log_2 10 \rfloor} − 1 and 8 = 2^{\lfloor \log_2 10 \rfloor} on the top row. Now the boundary is not between them because the missing number has most significant bit 0, so the boundary is shifted one position to the left in comparison with A. However, if we do not know what the missing number's most significant bit is, we can deduce it is 0 from the fact that there are two 1's at positions 7 and 8 on the top row.

Clearly, if there were 0 and 1 at positions 7 and 8, respectively, on the top row, that would mean the missing number's most significant bit is 1, as in the following example where the array is called B, n = 10 and the missing number is 9 = 1001₂:

![](bbox=[0.24, 0.4, 0.76, 0.5])

So, by inspecting only position 2^{\lfloor \log_2 n \rfloor} − 1 on the top row, we can deduce the most significant bit of the missing number as follows:

$$\textit{the missing number's most significant bit} = \begin{cases} 0, & \text{if } A[0][2^{\lfloor \log_2 n \rfloor} - 1] == 1; \\ 1, & \text{if } A[0][2^{\lfloor \log_2 n \rfloor} - 1] == 0. \end{cases} \tag{2.6}$$

Having computed the most significant bit of the missing number in Θ(1) time, we compute the second most significant bit in Θ(1) time, etc., until we compute all bits of the missing number with Θ(log n) attempts, each taking Θ(1) time.

# ### Case 1

If the most significant bit is 0, to compute the second most significant bit we consider only the subarray of columns 0, 1, . . . , 2^{\lfloor \log_2 n \rfloor} − 2 and rows 1, 2, . . . , ⌊log₂ n⌋. Using the above A as an example, that subarray is, say, A′: