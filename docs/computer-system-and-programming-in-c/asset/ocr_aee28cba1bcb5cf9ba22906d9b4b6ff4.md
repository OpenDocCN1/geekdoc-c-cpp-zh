switches inside a computing machine are tiny and they are able to turn on and off very rapidly. The binary notation system suits a computer majorly well.

16384, 32768 (powers of two) for the conversion.

# Binary to Decimal Conversion

+   - To convert binary into decimal is very simple and can be done as shown below:
+   - Say we want to convert the 8 bit value **10011101** into a decimal value, we can use a formula like that below:

![](bbox=[0.123, 0.285, 0.454, 0.327])

As you can see we have placed the numbers 1, 2, 4, 8, 16, 32, 64, 128 (powers of two) in reverse numerical order and then written the binary value below. To convert you simply take a value from the top row wherever there is a 1 below and add the values together, for instance in our example we would have 128 + 16 + 8 + 4 + 1 = 157. For a 16 bit value you would get a sum of the following values: 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768 (powers of two) for the conversion.

Because we know binary is base 2 then the above could be written as:

1*2^7 + 0*2^6 + 0*2^5 + 1*2^4 + 1*2^3 + 1*2^2 + 0*2^1 + 1*2^0 = 157.

# Example 1

Convert binary **11101** to decimal

Basically, this is the same as saying:

1*(2^4) + 1*(2^3) + 1*(2^2) + 0*(2^1) + 1*(2^0)

or

1*(16) + 1*(8) + 1*(4) + 0*(2) + 1*(1)

The reason it's easier to start backward is because:

+   - Counting the number of digits takes extra time, and you might count wrongly.
+   - If you do not remember what a particular power-of-2 value, it is easy to calculate it from the previous value. For instance, if you do not recall what the value of 2*2*2 is, then just double the value of 2*2.

| Notes | Multiplication | Result |
|---|---:|---:|
| start from the last digit, which is 1, multiply that digit with 2^0, note that the power of 0 of any number is always 1 | 1*(2^0) | 1 |
| 11101 (current digit is in bold) |  |  |
| process the previous digit, which is 0, multiply that digit with the increasing power of 2 | 0*(2^1) | 0 |
| 11101 (current digit is in bold) |  |  |
| process the previous digit, which is 1, note that 2^2 means 2*2 | 1*(2^2) | 4 |
| 11101 (current digit is in bold) |  |  |
| process the previous digit, which is 1, note that 2^3 means 2*2*2 | 1*(2^3) | 8 |
| 11101 (current digit is in bold) |  |  |
| process the previous digit, which is 1, note that 2^4 means 2*2*2*2 | 1*(2^4) | 16 |
| 11101 (current digit is in bold) |  |  |
| here, we stop because there is no more digit to process |  |  |
| this number comes from the sum of the RESULTS | ANSWER | 29 |