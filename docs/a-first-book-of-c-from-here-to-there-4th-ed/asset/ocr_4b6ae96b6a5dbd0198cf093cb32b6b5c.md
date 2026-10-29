accommodate special situations (such as a very small or large range of numbers) and have been retained for historical reasons. They enabled programmers to maximize memory usage by selecting the data type using the smallest amount of memory, consistent with an application’s requirements. When computer memories were small and expensive, compared with today’s computers, the amount of memory used was a major concern. Although no longer a concern for most programs, these types still allow programmers to optimize memory usage when necessary. This optimization is often required in engineering applications, such as control systems used in home appliances and automobiles.

![](bbox=[0.38, 0.33, 0.77, 0.57])

Figure 2.2 C++ integer data types

# The int Data Type

The values supported by the int data type are whole numbers, which are mathematically known as integers. An integer value consists of digits only and can optionally be preceded by a plus (+) or minus (−) sign. Therefore, an integer value can be the number 0 or any positive or negative number without a decimal point. The following are examples of valid integers:

0      -10      1000      -26351
5      +25      253       +36

As these examples show, integers can contain an explicit sign. However, no commas, decimal points, or special symbols, such as the dollar sign, are allowed, as in these examples of invalid integers:

$255.62    3.      1,492.89
2,523      6,243,892    +6.0

Compilers differ in their internal limit on the largest (most positive) and smallest (most negative) integer values that can be stored in each data type.¹ The most common storage allocation is 4 bytes for the int data type, which restricts the values used to represent integers from -2,147,483,648 to 2,147,483,647.²

¹The limits the compiler imposes are found in the limits header file and defined as the constants INT_MIN and INT_MAX.
²The magnitude of the most negative number is always one more than the magnitude of the most positive number. The reason is the two complement method of integer storage, described in Section 2.6.