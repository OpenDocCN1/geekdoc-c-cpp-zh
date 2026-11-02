
two floating point types. We talk more about Ada’s generic facilities in Sections 2.4.2 and 3.3.3.

## Fixed Point Types

As illustrated in Figure 2.1, Ada provides support for two representations of real numbers: fixed point and floating point. Fixed point numbers provide a fixed number of digits before and after the radix point. When we write a real number on paper, we usually use a fixed point format such as

12.75    0.00433    1258.1

In a floating point number, the radix point may “float” to any location. Floating point is the computer realization of scientific notation. A floating point value is implemented as two separate numbers: a mantissa and an exponent. The following are all valid representations of 1,285.1:

.12581 × 10⁴    1.2581 × 10³    12.581 × 10²  
125.81 × 10¹    1258.1 × 10⁰    12581. × 10⁻¹

Floating point is by far the more commonly used representation for real numbers. In most programming languages, floating point is the only type available for representing real numbers. Floating point types support a much wider range of values than fixed point types. However, fixed point types have two properties that favor their use in certain situations. First, fixed point arithmetic is performed with standard integer machine instructions. Integer instructions are typically faster than floating point instructions. Some inexpensive embedded microprocessors, microcontrollers, and digital signal processors do not support floating point arithmetic. In such cases, fixed point is the only efficient representation available for real numbers.

The second advantage of fixed point is that the maximum representational error is constant throughout the range of the type. The maximum representational error for a floating point type depends on the magnitude of the number. This difference is a result of the distribution of model numbers in each of the representations. The distance between model floating point numbers varies through the range; it depends on the value of the exponent. The distance between model fixed point numbers is constant throughout the range.

Figure 2.2 illustrates the difference in model number distributions. Figure 2.2a shows the model numbers for a very simple floating point representation. There are ten model numbers between 1.0 and 10.0, ten model numbers between 0.1 and 1.0, and ten model numbers between 0.01 and 0.1. Figure 2.2b shows the model numbers for a simple fixed point representation. The distance between model numbers is constant throughout the range. Figure 2.2 shows that the representational error for a floating point number gets larger as the number gets larger, whereas the representational error for a fixed point number is constant throughout its range.

![](img/d1a16034f5d1724d114fe7293dc71133_53_0.png)

a. A simple floating point type (digits = 1)

![](img/d1a16034f5d1724d114fe7293dc71133_53_1.png)

b. A simple fixed point type (delta = 0.25)

**Figure 2.2. Distribution of model numbers.**

Does the choice of real number representation really make a difference in our applications? “On February 25, 1991, a Patriot missile defense system operating at Dhahran, Saudi Arabia, during Operation Desert Storm failed to track and intercept an incoming Scud [missile]. This Scud subsequently hit an Army barracks, killing 28 Americans” Blair, Obenski, and Bridickas (1992). The Patriot battery failed because of a software problem related to the storage and use of floating point numbers. The system stored time, in tenths of a second, in a floating point variable. Table 2.1, taken from the Government Accounting Office report, shows the magnitude of the error in representing this time as a floating point value. As with all floating point representations, the magnitude of the error increases with the magnitude of the value.

**Table 2.1. Magnitude of range gate error when modeling time as a floating point real number**

| Hours | Seconds | Absolute inaccuracy (Seconds) | Approximate shift in missile range gate (Meters) |
|---|---|---|---|
| 0 | 0.0 | 0.0 | 0 |
| 1 | 3600.0 | 0.0034 | 7 |
| 8 | 28800.0 | 0.0275 | 55 |
| 20 | 72000.0 | 0.0687 | 137 |
| 48 | 172800.0 | 0.1648 | 330 |
| 72 | 259200.0 | 0.2472 | 494 |
| 100 | 360000.0 | 0.3433 | 687 |

Table 2.1 shows that the floating point representation error grows as the number grows. After twenty hours, the time is off enough that the target is outside the range gate and the Patriot missile fails to launch against a threat. After the tragedy, the software was corrected by replacing the floating point time variables with fixed point variables. Let us note that Ada's predefined type Duration is a fixed point type for seconds.

To declare a fixed point type, we specify the maximum distance between model numbers that we are willing to accept. The maximum representational error is half of this distance. We may also specify an optional range for the type. Here are two examples:

```
type Thirds is delta 1.0 / 3.0  range 0.0 .. 100_000.0;
type Volts  is delta 2.0**(-12) range 0.0 .. 5.0;
```

Thirds is a fixed point type with a specified distance of $\frac{1}{3}$ (0.33333...) between model numbers and Volts is a fixed point type with a specified distance of $\frac{1}{4096}$ (0.000244140625) between model numbers. Both of these types are called *ordinary fixed point types*. The actual distance between model numbers in our fixed point type may be smaller than our request. The actual distance between model numbers is the largest power of two that is less than or equal to the value given for delta. So although we specified a delta value of $\frac{1}{3}$ for Thirds, the actual delta used is the power of two, $\frac{1}{4}$ ($2^{-2}$). The delta we specified for Volts is a power of two so it is used directly. Because the distance between model numbers is some power of two, ordinary fixed point types are sometimes called *binary fixed point types*.

Neither floating point nor ordinary fixed point types are appropriate for currency calculations. Neither is capable of accurate storage of decimal fractions that are so important in commercial applications. Ada's *decimal fixed point types* are the more appropriate choice for such values. Here is an example:

```
type Dollars is delta 0.01 digits 12;
```

For decimal fixed point types, we must specify both a delta that is a power of ten and the number of decimal digits. A range is optional. A value of type Dollars contains twelve decimal digits. Because the distance between model numbers is 0.01, two of these digits are to the right of the decimal point, leaving ten digits for the left side of the decimal point.

We use the generic packages Ada.Text_IO.Fixed_IO and Ada.Text_IO.Decimal_IO to instantiate packages for the input and output of ordinary and decimal fixed point types. You may find the details for the available I/O operations in section A.10.9 of the ARM (2012). Here are the instantiations for our example types:

```
package Thirds_IO is new Ada.Text_IO.Fixed_IO (Thirds);
package Volts_IO  is new Ada.Text_IO.Fixed_IO (Volts);
package Dollar_IO is new Ada.Text_IO.Decimal_IO (Dollars);
```

Ada’s rules that prevent the mixing of different types are more relaxed for fixed point type multiplication and division. Multiplication and division are allowed between any two fixed point types. The type of the result is determined by the context. So, for example, if we assign the result of multiplying a Volts value and a Thirds value to a Volts variable, the result type of the multiplication would be Volts. Similarly, if we assign the same product to a Thirds variable, the result type of the multiplication would be Thirds. Additionally, a fixed point value may be multiplied or divided by an integer yielding the same fixed point type.

## 2.3.2 Discrete Types

Recall that a scalar type is an atomic type with the additional property of ordering. A discrete type is a scalar type with the additional property of unique successors and predecessors. The language-defined types Boolean, Character, and Integer are all discrete types. In the next sections we will look at defining our own discrete types.

### Enumeration Types

An enumeration type provides a means for defining a type by enumerating (listing) all the values in the domain. The following program illustrates the definition and use of three enumeration types:

```
with Ada.Text_IO;              use Ada.Text_IO;
with Ada.Integer_Text_IO;      use Ada.Integer_Text_IO;
procedure Enum_Example is
   -- Declaration of three enumeration types
   type Day_Type is (Monday, Tuesday, Wednesday, Thursday,
                     Friday, Saturday, Sunday);
   type Traffic_Light_Color is (Red, Green, Yellow);
   type Pixel_Color        is (Red, Green, Blue, Cyan,
                               Magenta, Yellow, Black, White);

   package Day_IO is new Ada.Text_IO.Enumeration_IO (Day_Type);

   function Next_Day (Day : in Day_Type) return Day_Type is
   begin
```
