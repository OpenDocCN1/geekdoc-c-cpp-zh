```
return source.Aggregate(
  // seed - array of three doubles constructed
  // using double factory function, initialized to 0
  () => new double[3] { 0.0, 0.0, 0.0 },

  // item aggregation function, run for each element
  (subtotal, item) => {
    subtotal[0]++; // count
    subtotal[1] += item; // sum
    // sum of squares
    subtotal[2] += (double)item * (double)item;
    return subtotal;
  },

  // combine function,
  // run on completion of each "thread"
  (total, thisThread) => {
    total[0] += thisThread[0];
    total[1] += thisThread[1];
    total[2] += thisThread[2];
    return total;
  },

  // result selector function
  // finess the final sum into the variance
  // mean = sum / count
  // variance = (sum_sq - sum * mean) / (n - 1)

  // Sources with zero or one element return a value of 0
  (result) => (result[0] > 0 ?
    result[2] - result[1] * (result[1] / result[0])
    / (result[0] - 1) : 0.0
);

public static double StandardDeviation(
  this ParallelQuery<int> source) {
  return Math.Sqrt(source.Variance());
}
```