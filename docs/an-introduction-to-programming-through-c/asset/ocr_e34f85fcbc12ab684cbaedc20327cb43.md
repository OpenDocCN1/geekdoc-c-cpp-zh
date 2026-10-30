So from this, we can find its Taylor series. Clearly f'(x) = 1/x. f''(x) = -1/x² and so on. It is convenient to use x₀ = 1. Thus we get:

ln 1 + h = h - h²/2 + h³/3 - h⁴/4 …

A very important point to note for this series is that the series is valid only for -1 < h ≤ 1. We noted earlier that the Taylor series is valid only if x is close enough to x₀, or equivalently x - x₀ = h is small. For the ln function, we have a precise description of what close enough means: within a unit distance from x₀.

Even so, note that you can indeed use the series to calculate ln x for arbitrary values of x. Simply observe that ln x = 1 + ln x/e. Thus by factoring out powers of e we will need to use the series only on a number smaller than 1.

# 8.1.3 Some general remarks

Note that the Taylor series is often written as

f(x₀ + h) = f(x₀) + f'(x₀)h + f''(x₀) h²/2! + f'''(x₀) h³/3! + …

If we choose x₀ = 0, we get the McLaurin series, which is

f(x) = f(0) + f'(0)x + f''(0) x²/2! + f'''(0) x³/3! + …

In general, the terms of the Taylor series increase with x. Thus, it is best to keep x small if possible. For example, suppose we wish to compute sin(100.0). One possibility is to use the previous program specifying 100.0 as input. A better way is to subtract as many multiples of 2π as possible, since we know that sin(x + 2nπ) = sin(x) for any integer n. In fact identities such as sin(x) = -sin(π - x) can be used to further reduce the value used in the main loop of the program. In fact, noting that the Taylor series for cos(x) is:

cos(x) = 1 - x²/2! + x⁴/4! - x⁶/6! + …

we can in fact compute the sine using sin(x) = cos(π/2 - x) if π/2 - x happens to be smaller in absolute value than x.

The proof of the Taylor series expansion is well beyond the scope of this book. However, we have provided some intuitive justification for the first two terms by considering the tangent to approximate the function curve, Figure 8.1.¹

> ¹ You might be familiar with the formula s(t) = ut + ½ a t², in which s(t) is the distance covered in time t by a particle moving at a constant acceleration a, with initial velocity u. Note that u = s'(0), a = s''(0) and with this substitution the formula can be written as s(t) = s(0) + s'(0)t + s''(0) t²/2, which resembles the Taylor series in the first 3 terms.