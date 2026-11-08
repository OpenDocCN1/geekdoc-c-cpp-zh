# Comparing Pointers

You can safely compare pointers of the same type using the familiar `==`, `!=`, `<`, `<=`, `>`, and `>=` operators. The outcome of these comparisons will of course be compatible with your intuitions about pointer and integer arithmetic. Using the same variables as before, the expression `pnum2 < pnum1` will thus evaluate to true, as `pnum2 - pnum1 < 0` as well (pnum2 - pnum1 equals -5). In other words, the further the pointers in the array or the higher the index of the element it points to, the larger the pointer is.

# Using Pointer Notation with an Array Name

You can use an array name as though it was a pointer for addressing the array elements. Suppose you define this array:

```
long data[5] {};
```

You can refer to the element data[3] using pointer notation as `*(data + 3)`. This notation can be applied generally so that corresponding to the elements data[0], data[1], data[2], ..., you can write *data, *(data + 1), *(data + 2), and so on. The array name by itself refers to the address of the beginning of the array, so an expression such as data+2 produces the address of the element two elements along from the first.

You can use pointer notation with an array name in the same way as you use an index between square brackets—in expressions or on the left of an assignment. You could set the values of the data array to even integers with this loop:

```
for (size_t i {}; i < std::size(data); ++i)
{
  *(data + i) = 2 * (i + 1);
}
```

The expression `*(data + i)` refers to successive elements of the array. The loop will set the values of the five array elements to 2, 4, 6, 8, and 10. You could sum the elements of the array like this:

```
long sum {};
for (size_t i {}; i < std::size(data); ++i)
{
  sum += *(data + i);
}
```

Let’s try some of this in a practical context that has a little more meat. This example calculates prime numbers (a prime number is an integer that is divisible only by 1 and itself). Here’s the code:

```
// Ex6_05.cpp
// Calculating primes using pointer notation
import <iostream>;
import <format>;

int main()
{
  const size_t max {100};    // Number of primes required
  long primes[max] {2L};     // First prime defined
  size_t count {1};          // Count of primes found so far
  long trial {3L};           // Candidate prime
```