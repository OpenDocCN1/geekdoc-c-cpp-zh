two floating point types. We talk more about Ada’s generic facilities in Sections 2.4.2 and 3.3.3.

# Fixed Point Types

As illustrated in Figure 2.1, Ada provides support for two representations of real numbers: fixed point and floating point. Fixed point numbers provide a fixed number of digits before and after the radix point. When we write a real number on paper, we usually use a fixed point format such as

12.75    0.00433    1258.1

In a floating point number, the radix point may “float” to any location. Floating point is the computer realization of scientific notation. A floating point value is implemented as two separate numbers: a mantissa and an exponent. The following are all valid representations of 1,285.1:

.12581 × 10⁴    1.2581 × 10³    12.581 × 10²
125.81 × 10¹    1258.1 × 10⁰    12581. × 10⁻¹

Floating point is by far the more commonly used representation for real numbers. In most programming languages, floating point is the only type available for representing real numbers. Floating point types support a much wider range of values than fixed point types. However, fixed point types have two properties that favor their use in certain situations. First, fixed point arithmetic is performed with standard integer machine instructions. Integer instructions are typically faster than floating point instructions. Some inexpensive embedded microprocessors, microcontrollers, and digital signal processors do not support floating point arithmetic. In such cases, fixed point is the only efficient representation available for real numbers.

The second advantage of fixed point is that the maximum representational error is constant throughout the range of the type. The maximum representational error for a floating point type depends on the magnitude of the number. This difference is a result of the distribution of model numbers in each of the representations. The distance between model floating point numbers varies through the range; it depends on the value of the exponent. The distance between model fixed point numbers is constant throughout the range.

Figure 2.2 illustrates the difference in model number distributions. Figure 2.2a shows the model numbers for a very simple floating point representation. There are ten model numbers between 1.0 and 10.0, ten model numbers between 0.1 and 1.0, and ten model numbers between 0.01 and 0.1. Figure 2.2b shows the model numbers for a simple fixed point representation. The distance between model numbers is constant throughout the range. Figure 2.2 shows