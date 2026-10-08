automatically by the C compiler, or a programmer can ask the compiler to temporarily convert it to the desired data type. The automatic conversion done by the C compiler is known as type conversion, while the conversion in which a programmer asks the compiler to temporarily convert the datatype of an operand is known as type casting. Program 4 uses automatic type conversion. The evaluation of expression f_area = (i_base * i_height) / 2.0 is shown in Figure 3:

![](bbox=[0.38, 0.24, 0.68, 0.38])

▲ Figure 3: Automatic Type Conversion

The expression evaluation in C also follows the Brackets Order Division Multiply Add Subtract (BODMAS) rule. It can be seen in Figure 3 that first the subexpression i_base * i_height is evaluated; it will result to an integer value. The next operation is division by 2.0; however, before performing this operation, the compiler converts the result of multiplication into a float value, as shown in Figure 3. Finally, the result is then assigned to the variable f_area. The internal conversion (implicit conversion) of data types is performed in the order as shown in Figure 4:

![](bbox=[0.41, 0.52, 0.62, 0.72])

▲ Figure 4: Conversion Order of Data Types

Figure 4 shows that C language converts the data type in order of lower space requirement to higher space requirements. The bytes shown in the figure may vary from compiler to compiler, but the order will remain the same.

A programmer can explicitly convert the data type of any variable used in the expression by using a process called type casting. When type casting is applied to an operand, it overrides the internal conversion performed by the compiler. To type cast a variable used