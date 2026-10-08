# 10.7 (Set of Integers)

Create class IntegerSet. Each IntegerSet object can hold integers in the

0–100. The set is represented by an array of bools. Array a[i] is true if integer i is in the set. Array a[]] is false if integer j is not in the set. The parameterless constructor initializes the "empty set" (i.e., a set whose array representation contains all false values).

Provide the following methods:

+   a) Union creates a set that is the set-theoretic union of two existing sets (i.e., an element of the third set's array is true if it is true in either or of the existing sets—otherwise, the element of the third is set to false).

+   b) Intersection creates a set which is the set-theoretic intersection of two existing sets (i.c., an element of the third set's array is false if element is false in either or both of the existing sets—otherwise, the element of the third is set to true).

+   c) Insert inserts a new integer k into a set (by setting a[k] to true).

+   d) Delete deletes integer m (by setting a[m] to false).

+   e) ToString returns a string containing the set as a list of numbers separated by spaces. Include only those elements that are present in the set. Use -- to represent an empty set.

+   f) Equals determines whether two sets are equal.

Write an app to test class IntegerSet. Instantiate IntegerSet objects. Test that all methods work properly.

# 10.8 (Rational Numbers)

Create a class Rational for performing arithmetic with fractions. Write an app to test it. Use integer variables to represent the private instance variables of the class--the numerator and the denominator. Provide a constructor that enables an object of this class to be initialized when it's reduced. The constructor should store the fraction in reduced form.

The fraction 2/4

is equivalent to 1/2 and should be stored in the object as 1 in the numerator and 2 in the denominator. Provide a parameterless constructor with default values in case no initializers are provided. Provide public methods that perform each of the following operations (calculation results should be stored in a reduced form):

+   a) Add Rational numbers.

+   b) Subtract Rational numbers.

+   c) Multiply Rational numbers.

+   d) Divide Rational numbers.

+   e) Display Rational numbers in the form a/b, where a is the numerator and b is the denominator.

+   f) Display Rational numbers in floating-point format. (Consider formatting capabilities that enable the user to specify the number of digits of precision to the right of the decimal point).

# 10.9 (HugeInteger Class)

Create class HugeInteger that uses a 40-element array of digits to store integers as large as 40 digits. Provide methods Input, ToString, Add, and Subtract. For comparing HugeInteger, provide the following methods: EqualsTo, NotEqualTo, IsLessThan, IsGreaterOrEqualTo, and IsLessThanOrEqualTo. Each of a method returns true if the relationship holds between the two HugeInteger objects and returns false if the relationship does not hold. Provide IsZero. If you feel ambitious, provide methods Multiply, Divide, and Remainder.

In the Input method, use the method ToCharArray to convert the input into an array of characters, iterate through these characters to create your HugeInteger. If you feel ambitious, provide methods Multiply, Divide, and Remainder. [Note: .NET Framework Class Library includes BigInteger for arbitrary sized integers.]