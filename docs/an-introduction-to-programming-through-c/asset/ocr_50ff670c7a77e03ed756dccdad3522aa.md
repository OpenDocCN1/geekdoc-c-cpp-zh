# 8.1.1 Sine of an angle

As an example, consider f(x) = sin(x), where x is in radians. Then choosing x0 = 0 we know f(x0) = 0. We know that f'(x) = cos(x), f''(x) = −sin(x), f'''(x) = −cos(x) and so on. Since cos(0) = 1, we know the exact value of every derivative, it is either 0, 1 or -1. Thus we get

sin(x) = x − x³/3! + x⁵/5! − x⁷/7! + x⁹/9! − …

Here the angle x is in radians. When a series has alternating positive and negative terms, and the terms get closer and closer to 0 for any fixed x, then it turns out that the error in taking just the first k terms is at most the k + 1th term (absolute value). The kth term of our series is (−1)^{k+1} x^{2k−1}/(2k−1)!. Thus if we want the error to be ε then we should ensure x^{2k+1}/(2k+1)! ≤ ε.

We have already seen how to sum series (Section 4). Clearly we will need a loop, in the kth iteration of which we will calculate the series to k terms. We must terminate the loop if the last added term is smaller than our target ε. We can calculate the kth term tk from scratch in the kth iteration, but it is useful to note the following relationship:

tk = (−1)^{k+1} x^{2k−1}/(2k−1)! = tk−1 ( (−1) x² / ((2k−2)(2k−1)) )

provided k > 1. If k = 1 then tk = 1, of course, and we dont use the above relationship. Thus within the loop we only compute the terms for k = 2,3,… as needed. Thus our code becomes:

```
main_program{
    double x; cin >> x;

    double epsilon = 1.0E-20, sum = x, term = x;

    for(int k=2; abs(term) > epsilon; k++){
        // Plan: term = t_{k-1}, sum = sum of k-1 terms
        term *= -x * x / ((2*k-2)*(2*k-1));
        sum += term;
    }

    cout << sum << endl;
}
```

The command abs stands for absolute value, and returns the absolute value of its argument.

# 8.1.2 Natural log

Consider f(x) = ln x, the natural logarithm of x. One way of defining it is

ln x = ∫₁ˣ 1/u du