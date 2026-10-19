```
Visual Basic Example of Multiplying a Loop Index
For i = 0 to saleCount - 1
    commission(i) = (i + 1) * revenue * baseCommission * discount
Next
```

This code is straightforward but expensive. You can rewrite the loop so that you accumulate multiples rather than computing them each time. This reduces the strength of the operations from multiplication to addition.

```
Visual Basic Example of Adding Rather Than Multiplying
incrementalCommission = revenue * baseCommission * discount
cumulativeCommission = incrementalCommission
For i = 0 to saleCount - 1
    commission(i) = cumulativeCommission
    cumulativeCommission = cumulativeCommission + incrementalCommission
Next
```

Multiplication is expensive, and this kind of change is like a manufacturer’s coupon that gives you a discount on the cost of the loop. The original code incremented i each time and multiplied it by revenue * baseCommission * discount—first by 1, then by 2, then by 3, and so on. The optimized code sets incrementalCommission equal to revenue * baseCommission * discount. It then adds incrementalCommission to cumulativeCommission on each pass through the loop. On the first pass, it’s been added once; on the second pass, it’s been added twice; on the third pass, it’s been added three times; and so on. The effect is the same as multiplying incrementalCommission by 1, then by 2, then by 3, and so on, but it’s cheaper.

The key is that the original multiplication has to depend on the loop index. In this case, the loop index was the only part of the expression that varied, so the expression could be recoded more economically. Here’s how much the rewrite helped in some test cases:

| Language | Straight Time | Code-Tuned Time | Time Savings |
|---|---|---|---|
| C++ | 4.33 | 3.80 | 12% |
| Visual Basic | 3.54 | 1.80 | 49% |
| Note: Benchmark performed with saleCount equals 20. All computed variables are floating point. |

# 26.3 Data Transformations

Changes in data types can be a powerful aid in reducing program size and improving execution speed. Data-structure design is outside the scope of this book, but modest changes in the implementation of a specific data type can also improve performance. Here are a few ways to tune your data types.