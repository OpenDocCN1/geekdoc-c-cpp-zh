x reads the value 0 (line 10) but y reads the value 11 (line 9). This happens, although the writing of x (line 5) is sequenced before the writing of y (line 6).

# 6.4.7 Conclusion

Using a small program and successively improve it was quite enlightening. First, with each step, more interleavings of threads were possible; therefore, more different values for x and y were possible. Second, the challenge of the program increases with each improvement. Even for this small program, CppMem provides invaluable services.