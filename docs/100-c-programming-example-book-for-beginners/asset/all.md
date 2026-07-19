![](image_rsrc27X.jpg)

100 C PROGRAM EXAMPLES

Written by – Devbrat Rudra

1\. Hello World Program:

#include <stdio.h>

int main() {

printf("Hello, World!");

return 0;

}

2\. Add Two Numbers:

#include <stdio.h>

int main() {

int a, b, sum;

printf("Enter two numbers: ");

scanf("%d %d", &a, &b);

sum = a + b;

printf("Sum: %d", sum);

return 0;

}

3\. Factorial of a Number:

#include <stdio.h>

int main() {

int n, i;

unsigned long long fact = 1;

printf("Enter an integer: ");

scanf("%d", &n);

for (i = 1; i <= n; ++i) {

fact *= i;

}

printf("Factorial: %llu", fact);

return 0;

}

4\. Fibonacci Series:

#include <stdio.h>

int main() {

int n, first = 0, second = 1, next, i;

printf("Enter the number of terms: ");

scanf("%d", &n);

printf("Fibonacci Series: ");

for (i = 0; i < n; i++) {

if (i <= 1)

next = i;

else {

next = first + second;

first = second;

second = next;

}

printf("%d ", next);

}

return 0;

}

5\. Check Prime Number:

#include <stdio.h>

#include <stdbool.h>

bool isPrime(int n) {

if (n <= 1)

return false;

for (int i = 2; i * i <= n; i++) {

if (n % i == 0)

return false;

}

return true;

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isPrime(num))

printf("%d is a prime number.", num);

else

printf("%d is not a prime number.", num);

return 0;

}

SET-2

1\. Check Even or Odd:

#include <stdio.h>

int main() {

int num;

printf("Enter an integer: ");

scanf("%d", &num);

if (num % 2 == 0)

printf("%d is even.", num);

else

printf("%d is odd.", num);

return 0;

}

2\. Print Multiplication Table:

#include <stdio.h>

int main() {

int n, i;

printf("Enter an integer: ");

scanf("%d", &n);

for (i = 1; i <= 10; i++) {

printf("%d * %d = %d\n", n, i, n * i);

}

return 0;

}

3\. Calculate Simple Interest:

#include <stdio.h>

int main() {

float principle, rate, time, SI;

printf("Enter principle, rate and time: ");

scanf("%f %f %f", &principle, &rate, &time);

SI = (principle * rate * time) / 100;

printf("Simple Interest = %f", SI);

return 0;

}

4\. Celsius to Fahrenheit Conversion:

#include <stdio.h>

int main() {

float celsius, fahrenheit;

printf("Enter temperature in Celsius: ");

scanf("%f", &celsius);

fahrenheit = (celsius * 9 / 5) + 32;

printf("Temperature in Fahrenheit: %f", fahrenheit);

return 0;

}

5\. Find the Largest Among Three Numbers:

#include <stdio.h>

int main() {

double num1, num2, num3;

printf("Enter three numbers: ");

scanf("%lf %lf %lf", &num1, &num2, &num3);

if (num1 >= num2 && num1 >= num3)

printf("%.2f is the largest number.", num1);

else if (num2 >= num1 && num2 >= num3)

printf("%.2f is the largest number.", num2);

else

printf("%.2f is the largest number.", num3);

return 0;

}

SET-3

1\. Check Leap Year:

#include <stdio.h>

#include <stdbool.h>

bool isLeapYear(int year) {

if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0)

return true;

else

return false;

}

int main() {

int year;

printf("Enter a year: ");

scanf("%d", &year);

if (isLeapYear(year))

printf("%d is a leap year.", year);

else

printf("%d is not a leap year.", year);

return 0;

}

2\. Calculate Power of a Number:

#include <stdio.h>

int power(int base, int exponent) {

int result = 1;

for (int i = 0; i < exponent; i++) {

result *= base;

}

return result;

}

int main() {

int base, exponent;

printf("Enter base and exponent: ");

scanf("%d %d", &base, &exponent);

printf("Result: %d", power(base, exponent));

return 0;

}

3\. Reverse a Number:

#include <stdio.h>

int main() {

int num, reversed = 0, remainder;

printf("Enter an integer: ");

scanf("%d", &num);

while (num != 0) {

remainder = num % 10;

reversed = reversed * 10 + remainder;

num /= 10;

}

printf("Reversed number: %d", reversed);

return 0;

}

4\. Swap Two Numbers:

#include <stdio.h>

int main() {

int x, y, temp;

printf("Enter two numbers: ");

scanf("%d %d", &x, &y);

printf("Before swapping: x = %d, y = %d\n", x, y);

temp = x;

x = y;

y = temp;

printf("After swapping: x = %d, y = %d", x, y);

return 0;

}

5\. Calculate GCD (Greatest Common Divisor):

#include <stdio.h>

int gcd(int a, int b) {

if (b == 0)

return a;

else

return gcd(b, a % b);

}

int main() {

int num1, num2;

printf("Enter two integers: ");

scanf("%d %d", &num1, &num2);

printf("GCD of %d and %d is %d", num1, num2, gcd(num1, num2));

return 0;

}

SET-4

1\. Sum of Natural Numbers:

#include <stdio.h>

int main() {

int n, i, sum = 0;

printf("Enter a positive integer: ");

scanf("%d", &n);

for (i = 1; i <= n; ++i) {

sum += i;

}

printf("Sum = %d", sum);

return 0;

}

2\. Print Array Elements:

#include <stdio.h>

int main() {

int arr[] = {1, 2, 3, 4, 5};

int i;

printf("Array elements are: ");

for (i = 0; i < 5; i++) {

printf("%d ", arr[i]);

}

return 0;

}

3\. Calculate Area of a Circle:

#include <stdio.h>

int main() {

float radius, area;

printf("Enter the radius of the circle: ");

scanf("%f", &radius);

area = 3.14 * radius * radius;

printf("Area = %f", area);

return 0;

}

4\. String Length:

#include <stdio.h>

#include <string.h>

int main() {

char str[100];

printf("Enter a string: ");

gets(str);

int length = strlen(str);

printf("Length of the string: %d", length);

return 0;

}

5\. Print ASCII Value of a Character:

#include <stdio.h>

int main() {

char c;

printf("Enter a character: ");

scanf("%c", &c);

printf("ASCII value of %c is %d", c, c);

return 0;

}

SET-5

1\. Calculate the Area of a Triangle:

#include <stdio.h>

int main() {

float base, height, area;

printf("Enter the base and height of the triangle: ");

scanf("%f %f", &base, &height);

area = 0.5 * base * height;

printf("Area of the triangle = %f", area);

return 0;

}

2\. Calculate the Sum of Digits of a Number:

#include <stdio.h>

int main() {

int num, digit, sum = 0;

printf("Enter a number: ");

scanf("%d", &num);

while (num > 0) {

digit = num % 10;

sum += digit;

num /= 10;

}

printf("Sum of digits = %d", sum);

return 0;

}

3\. Check Armstrong Number:

#include <stdio.h>

#include <math.h>

int main() {

int num, originalNum, remainder, n = 0, result = 0;

printf("Enter an integer: ");

scanf("%d", &num);

originalNum = num;

while (originalNum != 0) {

originalNum /= 10;

++n;

}

originalNum = num;

while (originalNum != 0) {

remainder = originalNum % 10;

result += pow(remainder, n);

originalNum /= 10;

}

if (result == num)

printf("%d is an Armstrong number.", num);

else

printf("%d is not an Armstrong number.", num);

return 0;

}

4\. Print the Fibonacci Series using Recursion:

#include <stdio.h>

int fibonacci(int n) {

if (n <= 1)

return n;

return fibonacci(n - 1) + fibonacci(n - 2);

}

int main() {

int n, i;

printf("Enter the number of terms: ");

scanf("%d", &n);

printf("Fibonacci Series: ");

for (i = 0; i < n; i++) {

printf("%d ", fibonacci(i));

}

return 0;

}

5\. Calculate the Power using Recursion:

#include <stdio.h>

int power(int base, int exponent) {

if (exponent != 0)

return (base * power(base, exponent - 1));

else

return 1;

}

int main() {

int base, exponent;

printf("Enter base and exponent: ");

scanf("%d %d", &base, &exponent);

printf("Result: %d", power(base, exponent));

return 0;

}

SET-6

1\. Calculate the LCM (Least Common Multiple) of Two Numbers:

#include <stdio.h>

int gcd(int a, int b) {

if (b == 0)

return a;

return gcd(b, a % b);

}

int lcm(int a, int b) {

return (a * b) / gcd(a, b);

}

int main() {

int num1, num2;

printf("Enter two integers: ");

scanf("%d %d", &num1, &num2);

printf("LCM of %d and %d is %d", num1, num2, lcm(num1, num2));

return 0;

}

2\. Check if a Number is a Perfect Number:

#include <stdio.h>

int isPerfectNumber(int num) {

int sum = 0;

for (int i = 1; i <= num / 2; i++) {

if (num % i == 0) {

sum += i;

}

}

if (sum == num) {

return 1;

} else {

return 0;

}

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isPerfectNumber(num)) {

printf("%d is a perfect number.", num);

} else {

printf("%d is not a perfect number.", num);

}

return 0;

}

3\. Reverse an Array:

#include <stdio.h>

int main() {

int arr[] = {1, 2, 3, 4, 5};

int size = sizeof(arr) / sizeof(arr[0]);

printf("Original array: ");

for (int i = 0; i < size; i++) {

printf("%d ", arr[i]);

}

printf("\nReversed array: ");

for (int i = size - 1; i >= 0; i--) {

printf("%d ", arr[i]);

}

return 0;

}

4\. Find the Sum of Elements in an Array:

#include <stdio.h>

int main() {

int arr[] = {1, 2, 3, 4, 5};

int size = sizeof(arr) / sizeof(arr[0]);

int sum = 0;

for (int i = 0; i < size; i++) {

sum += arr[i];

}

printf("Sum of array elements: %d", sum);

return 0;

}

5\. Check if a Number is a Palindrome:

#include <stdio.h>

int isPalindrome(int num) {

int reversed = 0, original = num;

while (num != 0) {

int remainder = num % 10;

reversed = reversed * 10 + remainder;

num /= 10;

}

return original == reversed ? 1 : 0;

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isPalindrome(num)) {

printf("%d is a palindrome.", num);

} else {

printf("%d is not a palindrome.", num);

}

return 0;

}

SET-6

1\. Sort an Array in Ascending Order:

#include <stdio.h>

int main() {

int arr[] = {5, 2, 8, 1, 3};

int n = sizeof(arr) / sizeof(arr[0]);

int temp;

for (int i = 0; i < n; i++) {

for (int j = i + 1; j < n; j++) {

if (arr[i] > arr[j]) {

temp = arr[i];

arr[i] = arr[j];

arr[j] = temp;

}

}

}

printf("Array in ascending order: ");

for (int i = 0; i < n; i++) {

printf("%d ", arr[i]);

}

return 0;

}

2\. Check if a String is a Palindrome:

#include <stdio.h>

#include <string.h>

#include <stdbool.h>

bool isPalindrome(char str[]) {

int length = strlen(str);

for (int i = 0; i < length / 2; i++) {

if (str[i] != str[length - i - 1]) {

return false;

}

}

return true;

}

int main() {

char str[100];

printf("Enter a string: ");

gets(str);

if (isPalindrome(str)) {

printf("The string is a palindrome.");

} else {

printf("The string is not a palindrome.");

}

return 0;

}

3\. Count the Number of Vowels and Consonants in a String:

#include <stdio.h>

#include <string.h>

#include <ctype.h>

void countVowelConsonant(char str[]) {

int vowels = 0, consonants = 0;

for (int i = 0; i < strlen(str); i++) {

if (isalpha(str[i])) {

if (tolower(str[i]) == 'a' || tolower(str[i]) == 'e' || tolower(str[i]) == 'i' ||

tolower(str[i]) == 'o' || tolower(str[i]) == 'u') {

vowels++;

} else {

consonants++;

}

}

}

printf("Vowels: %d\n", vowels);

printf("Consonants: %d", consonants);

}

int main() {

char str[100];

printf("Enter a string: ");

gets(str);

countVowelConsonant(str);

return 0;

}

4\. Find the Largest Element in an Array:

#include <stdio.h>

int main() {

int arr[] = {5, 2, 8, 12, 3};

int n = sizeof(arr) / sizeof(arr[0]);

int max = arr[0];

for (int i = 1; i < n; i++) {

if (arr[i] > max) {

max = arr[i];

}

}

printf("Largest element in the array: %d", max);

return 0;

}

5\. Calculate the Power of a Number using a Function:

#include <stdio.h>

double power(double base, int exponent) {

double result = 1.0;

for (int i = 0; i < exponent; i++) {

result *= base;

}

return result;

}

int main() {

double base;

int exponent;

printf("Enter base and exponent: ");

scanf("%lf %d", &base, &exponent);

printf("Result: %lf", power(base, exponent));

return 0;

}

SET-7

1\. Find the Smallest Element in an Array:

#include <stdio.h>

int main() {

int arr[] = {5, 2, 8, 1, 3};

int n = sizeof(arr) / sizeof(arr[0]);

int min = arr[0];

for (int i = 1; i < n; i++) {

if (arr[i] < min) {

min = arr[i];

}

}

printf("Smallest element in the array: %d", min);

return 0;

}

2\. Print the HCF (Highest Common Factor) of Two Numbers:

#include <stdio.h>

int hcf(int a, int b) {

while (a != b) {

if (a > b) {

a -= b;

} else {

b -= a;

}

}

return a;

}

int main() {

int num1, num2;

printf("Enter two integers: ");

scanf("%d %d", &num1, &num2);

printf("HCF of %d and %d is %d", num1, num2, hcf(num1, num2));

return 0;

}

3\. Print Prime Numbers in a Given Interval:

#include <stdio.h>

#include <stdbool.h>

bool isPrime(int n) {

if (n <= 1)

return false;

for (int i = 2; i * i <= n; i++) {

if (n % i == 0)

return false;

}

return true;

}

int main() {

int start, end;

printf("Enter the starting and ending numbers: ");

scanf("%d %d", &start, &end);

printf("Prime numbers between %d and %d are: ", start, end);

for (int i = start; i <= end; i++) {

if (isPrime(i))

printf("%d ", i);

}

return 0;

}

4\. Check if a Number is a Perfect Square:

#include <stdio.h>

#include <math.h>

int isPerfectSquare(int num) {

int root = sqrt(num);

return root * root == num;

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isPerfectSquare(num)) {

printf("%d is a perfect square.", num);

} else {

printf("%d is not a perfect square.", num);

}

return 0;

}

5\. Check if a Number is a Strong Number:

#include <stdio.h>

int factorial(int num) {

int fact = 1;

for (int i = 1; i <= num; i++) {

fact *= i;

}

return fact;

}

int isStrongNumber(int num) {

int originalNum = num;

int sum = 0;

while (num > 0) {

int digit = num % 10;

sum += factorial(digit);

num /= 10;

}

return sum == originalNum;

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isStrongNumber(num)) {

printf("%d is a strong number.", num);

} else {

printf("%d is not a strong number.", num);

}

return 0;

}

SET-8

1\. Find the Sum of Natural Numbers using Recursion:

#include <stdio.h>

int sumOfNaturalNumbers(int n) {

if (n == 0) {

return 0;

}

return n + sumOfNaturalNumbers(n - 1);

}

int main() {

int num;

printf("Enter a positive integer: ");

scanf("%d", &num);

printf("Sum of first %d natural numbers is %d", num, sumOfNaturalNumbers(num));

return 0;

}

2\. Count the Number of Words in a String:

#include <stdio.h>

#include <string.h>

int countWords(char str[]) {

int count = 0;

for (int i = 0; str[i] != '\0'; i++) {

if (str[i] == ' ' && str[i + 1] != ' ') {

count++;

}

}

return count + 1;

}

int main() {

char str[100];

printf("Enter a string: ");

gets(str);

printf("Number of words in the string: %d", countWords(str));

return 0;

}

3\. Calculate the Average of Numbers in an Array:

#include <stdio.h>

int main() {

int arr[] = {5, 2, 8, 12, 3};

int n = sizeof(arr) / sizeof(arr[0]);

int sum = 0;

for (int i = 0; i < n; i++) {

sum += arr[i];

}

float average = (float)sum / n;

printf("Average of array elements: %f", average);

return 0;

}

4\. Find the Factorial of a Number using Recursion:

#include <stdio.h>

unsigned long long factorial(unsigned int num) {

if (num == 0) {

return 1;

}

return num * factorial(num - 1);

}

int main() {

int num;

printf("Enter a non-negative integer: ");

scanf("%d", &num);

printf("Factorial of %d = %llu", num, factorial(num));

return 0;

}

5\. Calculate the Area of a Rectangle:

#include <stdio.h>

int main() {

float length, width, area;

printf("Enter length and width of the rectangle: ");

scanf("%f %f", &length, &width);

area = length * width;

printf("Area of the rectangle = %f", area);

return 0;

}

SET-9

1\. Find the Sum of Elements in the Diagonal of a Matrix:

#include <stdio.h>

int main() {

int rows, cols, sum = 0;

printf("Enter the number of rows and columns of the matrix: ");

scanf("%d %d", &rows, &cols);

int matrix[rows][cols];

printf("Enter the elements of the matrix:\n");

for (int i = 0; i < rows; i++) {

for (int j = 0; j < cols; j++) {

scanf("%d", &matrix[i][j]);

if (i == j) {

sum += matrix[i][j];

}

}

}

printf("Sum of diagonal elements: %d", sum);

return 0;

}

2\. Find the Difference Between the Sum of Even and Odd Numbers in an Array:

#include <stdio.h>

int main() {

int arr[] = {5, 2, 8, 12, 3};

int n = sizeof(arr) / sizeof(arr[0]);

int sumEven = 0, sumOdd = 0;

for (int i = 0; i < n; i++) {

if (arr[i] % 2 == 0) {

sumEven += arr[i];

} else {

sumOdd += arr[i];

}

}

int difference = sumEven - sumOdd;

printf("Difference between the sum of even and odd numbers in the array: %d", difference);

return 0;

}

3\. Check if a Number is a Disarium Number:

#include <stdio.h>

#include <math.h>

int isDisarium(int num) {

int sum = 0, originalNum = num, digitCount = 0;

while (num > 0) {

num /= 10;

digitCount++;

}

num = originalNum;

while (num > 0) {

int digit = num % 10;

sum += pow(digit, digitCount);

num /= 10;

digitCount--;

}

return sum == originalNum;

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isDisarium(num)) {

printf("%d is a Disarium number.", num);

} else {

printf("%d is not a Disarium number.", num);

}

return 0;

}

4\. Print Pascal's Triangle:

#include <stdio.h>

long binomialCoeff(int n, int k) {

long res = 1;

if (k > n - k) {

k = n - k;

}

for (int i = 0; i < k; ++i) {

res *= (n - i);

res /= (i + 1);

}

return res;

}

void printPascalTriangle(int n) {

for (int line = 0; line < n; line++) {

for (int i = 0; i <= line; i++) {

printf("%ld ", binomialCoeff(line, i));

}

printf("\n");

}

}

int main() {

int rows;

printf("Enter the number of rows for Pascal's Triangle: ");

scanf("%d", &rows);

printPascalTriangle(rows);

return 0;

}

5\. Implement a Simple Calculator using Switch Case:

#include <stdio.h>

int main() {

char operator;

double num1, num2;

printf("Enter an operator (+, -, *, /): ");

scanf("%c", &operator);

printf("Enter two operands: ");

scanf("%lf %lf", &num1, &num2);

switch (operator) {

case '+':

printf("Result: %lf", num1 + num2);

break;

case '-':

printf("Result: %lf", num1 - num2);

break;

case '*':

printf("Result: %lf", num1 * num2);

break;

case '/':

if (num2 != 0) {

printf("Result: %lf", num1 / num2);

} else {

printf("Error! Division by zero.");

}

break;

default:

printf("Error! Invalid operator.");

}

return 0;

}

SET-10

1\. Sort an Array in Descending Order:

#include <stdio.h>

int main() {

int arr[] = {5, 2, 8, 1, 3};

int n = sizeof(arr) / sizeof(arr[0]);

int temp;

for (int i = 0; i < n; i++) {

for (int j = i + 1; j < n; j++) {

if (arr[i] < arr[j]) {

temp = arr[i];

arr[i] = arr[j];

arr[j] = temp;

}

}

}

printf("Array in descending order: ");

for (int i = 0; i < n; i++) {

printf("%d ", arr[i]);

}

return 0;

}

2\. Print a Hollow Rectangle Pattern:

#include <stdio.h>

int main() {

int rows, cols;

printf("Enter the number of rows and columns: ");

scanf("%d %d", &rows, &cols);

for (int i = 1; i <= rows; i++) {

for (int j = 1; j <= cols; j++) {

if (i == 1 || i == rows || j == 1 || j == cols)

printf("*");

else

printf(" ");

}

printf("\n");

}

return 0;

}

3\. Implement Bubble Sort:

#include <stdio.h>

void bubbleSort(int arr[], int n) {

for (int i = 0; i < n - 1; i++) {

for (int j = 0; j < n - i - 1; j++) {

if (arr[j] > arr[j + 1]) {

int temp = arr[j];

arr[j] = arr[j + 1];

arr[j + 1] = temp;

}

}

}

}

int main() {

int arr[] = {64, 34, 25, 12, 22, 11, 90};

int n = sizeof(arr) / sizeof(arr[0]);

bubbleSort(arr, n);

printf("Sorted array: ");

for (int i = 0; i < n; i++) {

printf("%d ", arr[i]);

}

return 0;

}

4\. Reverse a String:

#include <stdio.h>

#include <string.h>

void reverseString(char str[]) {

int length = strlen(str);

for (int i = 0; i < length / 2; i++) {

char temp = str[i];

str[i] = str[length - i - 1];

str[length - i - 1] = temp;

}

}

int main() {

char str[100];

printf("Enter a string: ");

gets(str);

reverseString(str);

printf("Reversed string: %s", str);

return 0;

}

5\. Convert Decimal to Binary:

#include <stdio.h>

long decimalToBinary(int n) {

long binaryNumber = 0;

int remainder, i = 1;

while (n != 0) {

remainder = n % 2;

n /= 2;

binaryNumber += remainder * i;

i *= 10;

}

return binaryNumber;

}

int main() {

int decimalNumber;

printf("Enter a decimal number: ");

scanf("%d", &decimalNumber);

printf("Binary equivalent: %ld", decimalToBinary(decimalNumber));

return 0;

}

SET-11

1\. Multiply Two Matrices:

#include <stdio.h>

int main() {

int m, n, p, q, c, d, k, sum = 0;

printf("Enter the number of rows and columns of the first matrix: ");

scanf("%d %d", &m, &n);

int first[m][n];

printf("Enter elements of the first matrix:\n");

for (c = 0; c < m; c++)

for (d = 0; d < n; d++)

scanf("%d", &first[c][d]);

printf("Enter the number of rows and columns of the second matrix: ");

scanf("%d %d", &p, &q);

if (n != p)

printf("Matrices with entered orders can't be multiplied with each other.");

else {

int second[p][q], multiply[m][q];

printf("Enter elements of the second matrix:\n");

for (c = 0; c < p; c++)

for (d = 0; d < q; d++)

scanf("%d", &second[c][d]);

for (c = 0; c < m; c++) {

for (d = 0; d < q; d++) {

for (k = 0; k < p; k++) {

sum = sum + first[c][k] * second[k][d];

}

multiply[c][d] = sum;

sum = 0;

}

}

printf("Product of the matrices:\n");

for (c = 0; c < m; c++) {

for (d = 0; d < q; d++)

printf("%d\t", multiply[c][d]);

printf("\n");

}

}

return 0;

}

2\. Find the Sum of Elements Above and Below the Main Diagonal in a Matrix:

#include <stdio.h>

int main() {

int rows, cols, sumAbove = 0, sumBelow = 0;

printf("Enter the number of rows and columns of the matrix: ");

scanf("%d %d", &rows, &cols);

int matrix[rows][cols];

printf("Enter the elements of the matrix:\n");

for (int i = 0; i < rows; i++) {

for (int j = 0; j < cols; j++) {

scanf("%d", &matrix[i][j]);

if (j > i) {

sumAbove += matrix[i][j];

} else if (j < i) {

sumBelow += matrix[i][j];

}

}

}

printf("Sum above the main diagonal: %d\n", sumAbove);

printf("Sum below the main diagonal: %d\n", sumBelow);

return 0;

}

3\. Calculate the Determinant of a 3x3 Matrix:

#include <stdio.h>

int main() {

int matrix[3][3];

int i, j;

long determinant = 0;

printf("Enter the 9 elements of the matrix: \n");

for (i = 0; i < 3; i++)

for (j = 0; j < 3; j++)

scanf("%d", &matrix[i][j]);

for (i = 0; i < 3; i++)

determinant = determinant + (matrix[0][i] * (matrix[1][(i + 1) % 3] * matrix[2][(i + 2) % 3] - matrix[1][(i + 2) % 3] * matrix[2][(i + 1) % 3]));

printf("The determinant of the 3x3 matrix is : %ld", determinant);

return 0;

}

4\. Calculate the Exponential of a Number:

#include <stdio.h>

long long int power(int base, int exponent) {

long long int result = 1;

for (int i = 0; i < exponent; i++) {

result *= base;

}

return result;

}

int main() {

int base, exponent;

printf("Enter base and exponent: ");

scanf("%d %d", &base, &exponent);

printf("Result: %lld", power(base, exponent));

return 0;

}

5\. Find the Transpose of a Matrix:

#include <stdio.h>

int main() {

int rows, cols, c, d;

printf("Enter the number of rows and columns of the matrix: ");

scanf("%d %d", &rows, &cols);

int matrix[rows][cols], transpose[cols][rows];

printf("Enter elements of the matrix:\n");

for (c = 0; c < rows; c++)

for (d = 0; d < cols; d++)

scanf("%d", &matrix[c][d]);

for (

c = 0; c < rows; c++)

for (d = 0; d < cols; d++)

transpose[d][c] = matrix[c][d];

printf("Transpose of the matrix:\n");

for (c = 0; c < cols; c++) {

for (d = 0; d < rows; d++)

printf("%d\t", transpose[c][d]);

printf("\n");

}

return 0;

}

SET-12

1\. Check if a Matrix is a Symmetric Matrix:

#include <stdio.h>

#define MAX 10

int main() {

int matrix[MAX][MAX];

int i, j, rows, cols, flag = 1;

printf("Enter number of rows and columns of matrix: ");

scanf("%d %d", &rows, &cols);

printf("Enter elements of the matrix:\n");

for (i = 0; i < rows; i++) {

for (j = 0; j < cols; j++) {

scanf("%d", &matrix[i][j]);

}

}

for (i = 0; i < rows; i++) {

for (j = 0; j < cols; j++) {

if (matrix[i][j] != matrix[j][i]) {

flag = 0;

break;

}

}

}

if (flag)

printf("The matrix is symmetric.\n");

else

printf("The matrix is not symmetric.\n");

return 0;

}

2\. Find the GCD (Greatest Common Divisor) of Two Numbers:

#include <stdio.h>

int gcd(int a, int b) {

if (b == 0)

return a;

return gcd(b, a % b);

}

int main() {

int num1, num2;

printf("Enter two positive integers: ");

scanf("%d %d", &num1, &num2);

printf("GCD of %d and %d is %d", num1, num2, gcd(num1, num2));

return 0;

}

3\. Print the Prime Factors of a Number:

#include <stdio.h>

void primeFactors(int num) {

while (num % 2 == 0) {

printf("%d ", 2);

num = num / 2;

}

for (int i = 3; i * i <= num; i = i + 2) {

while (num % i == 0) {

printf("%d ", i);

num = num / i;

}

}

if (num > 2)

printf("%d ", num);

}

int main() {

int num;

printf("Enter a positive integer: ");

scanf("%d", &num);

printf("Prime factors of %d are: ", num);

primeFactors(num);

return 0;

}

4\. Implement Quick Sort Algorithm:

#include <stdio.h>

void swap(int* a, int* b) {

int t = *a;

*a = *b;

*b = t;

}

int partition(int arr[], int low, int high) {

int pivot = arr[high];

int i = (low - 1);

for (int j = low; j <= high - 1; j++) {

if (arr[j] < pivot) {

i++;

swap(&arr[i], &arr[j]);

}

}

swap(&arr[i + 1], &arr[high]);

return (i + 1);

}

void quickSort(int arr[], int low, int high) {

if (low < high) {

int pi = partition(arr, low, high);

quickSort(arr, low, pi - 1);

quickSort(arr, pi + 1, high);

}

}

int main() {

int arr[] = {10, 7, 8, 9, 1, 5};

int n = sizeof(arr) / sizeof(arr[0]);

quickSort(arr, 0, n - 1);

printf("Sorted array: ");

for (int i = 0; i < n; i++) {

printf("%d ", arr[i]);

}

return 0;

}

5\. Find the Union and Intersection of Two Arrays:

#include <stdio.h>

void printUnion(int arr1[], int arr2[], int m, int n) {

int i = 0, j = 0;

printf("Union of the two arrays is: ");

while (i < m && j < n) {

if (arr1[i] < arr2[j])

printf("%d ", arr1[i++]);

else if (arr2[j] < arr1[i])

printf("%d ", arr2[j++]);

else {

printf("%d ", arr2[j++]);

i++;

}

}

while (i < m)

printf("%d ", arr1[i++]);

while (j < n)

printf("%d ", arr2[j++]);

}

void printIntersection(int arr1[], int arr2[], int m, int n) {

int i = 0, j = 0;

printf("\nIntersection of the two arrays is: ");

while (i < m && j < n) {

if (arr1[i] < arr2[j])

i++;

else if (arr2[j] < arr1[i])

j++;

else {

printf("%d ", arr2[j++]);

i++;

}

}

}

int main() {

int arr1[] = {1, 2, 4, 5, 6};

int arr2[] = {2, 3, 5, 7};

int m = sizeof(arr1) / sizeof(arr1[0]);

int n = sizeof(arr2) / sizeof(arr2[0]);

printUnion(arr1, arr2, m, n);

printIntersection(arr1, arr2, m, n);

return 0;

}

SET-13

1\. Generate Fibonacci Series up to a Certain Number:

#include <stdio.h>

void generateFibonacci(int n) {

int first = 0, second = 1, next;

printf("Fibonacci series up to %d terms: ", n);

for (int i = 1; i <= n; i++) {

printf("%d ", first);

next = first + second;

first = second;

second = next;

}

}

int main() {

int terms;

printf("Enter the number of terms: ");

scanf("%d", &terms);

generateFibonacci(terms);

return 0;

}

2\. Check if a Number is a Perfect Number:

#include <stdio.h>

int isPerfectNumber(int num) {

int sum = 0;

for (int i = 1; i <= num / 2; i++) {

if (num % i == 0) {

sum += i;

}

}

return sum == num;

}

int main() {

int num;

printf("Enter a positive integer: ");

scanf("%d", &num);

if (isPerfectNumber(num)) {

printf("%d is a perfect number.", num);

} else {

printf("%d is not a perfect number.", num);

}

return 0;

}

3\. Calculate the LCM (Least Common Multiple) of Two Numbers:

#include <stdio.h>

int gcd(int a, int b) {

if (b == 0)

return a;

return gcd(b, a % b);

}

int lcm(int a, int b) {

return (a * b) / gcd(a, b);

}

int main() {

int num1, num2;

printf("Enter two positive integers: ");

scanf("%d %d", &num1, &num2);

printf("LCM of %d and %d is %d", num1, num2, lcm(num1, num2));

return 0;

}

4\. Implement Linear Search:

#include <stdio.h>

int linearSearch(int arr[], int n, int key) {

for (int i = 0; i < n; i++) {

if (arr[i] == key)

return i;

}

return -1;

}

int main() {

int arr[] = {2, 3, 4, 10, 40};

int n = sizeof(arr) / sizeof(arr[0]);

int key = 10;

int result = linearSearch(arr, n, key);

(result == -1) ? printf("Element is not present in array")

: printf("Element is present at index %d", result);

return 0;

}

5\. Calculate the Power Set of a Set:

#include <stdio.h>

#include <math.h>

void printPowerSet(char *set, int set_size) {

unsigned int pow_set_size = pow(2, set_size);

int counter, j;

for (counter = 0; counter < pow_set_size; counter++) {

for (j = 0; j < set_size; j++) {

if (counter & (1 << j))

printf("%c", set[j]);

}

printf("\n");

}

}

int main() {

char set[] = {'a', 'b', 'c'};

printPowerSet(set, 3);

return 0;

}

SET-14

1\. Calculate the Area and Circumference of a Circle:

#include <stdio.h>

#define PI 3.14159

int main() {

float radius, area, circumference;

printf("Enter the radius of the circle: ");

scanf("%f", &radius);

area = PI * radius * radius;

circumference = 2 * PI * radius;

printf("Area of the circle = %f\n", area);

printf("Circumference of the circle = %f\n", circumference);

return 0;

}

2\. Implement a Binary Search Algorithm:

#include <stdio.h>

int binarySearch(int arr[], int left, int right, int key) {

while (left <= right) {

int mid = left + (right - left) / 2;

if (arr[mid] == key)

return mid;

if (arr[mid] < key)

left = mid + 1;

else

right = mid - 1;

}

return -1;

}

int main() {

int arr[] = {2, 3, 4, 10, 40};

int n = sizeof(arr) / sizeof(arr[0]);

int key = 10;

int result = binarySearch(arr, 0, n - 1, key);

(result == -1) ? printf("Element is not present in array")

: printf("Element is present at index %d", result);

return 0;

}

3\. Implement the Tower of Hanoi Problem:

#include <stdio.h>

void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod) {

if (n == 1) {

printf("Move disk 1 from rod %c to rod %c\n", from_rod, to_rod);

return;

}

towerOfHanoi(n - 1, from_rod, aux_rod, to_rod);

printf("Move disk %d from rod %c to rod %c\n", n, from_rod, to_rod);

towerOfHanoi(n - 1, aux_rod, to_rod, from_rod);

}

int main() {

int n = 4;

towerOfHanoi(n, 'A', 'C', 'B');

return 0;

}

4\. Calculate the Sine Series:

#include <stdio.h>

#include <math.h>

int main() {

float angle, radians, sum = 0;

printf("Enter the angle in degrees: ");

scanf("%f", &angle);

radians = angle * (3.14159 / 180);

for (int i = 0; i < 5; i++) {

sum += pow(-1, i) * pow(radians, 2 * i + 1) / tgamma(2 * i + 2);

}

printf("Sin(%f) = %f", angle, sum);

return 0;

}

5\. Find the Frequency of Characters in a String:

#include <stdio.h>

#define MAX_SIZE 100

int main() {

char str[MAX_SIZE];

int i, frequency[256] = {0};

printf("Enter a string: ");

fgets(str, MAX_SIZE, stdin);

for (i = 0; str[i] != '\0'; i++) {

frequency[str[i]]++;

}

printf("Character frequency:\n");

for (i = 0; i < 256; i++) {

if (frequency[i] != 0) {

printf("'%c' occurs %d times\n", i, frequency[i]);

}

}

return 0;

}

SET-15

1\. Calculate the Square Root of a Number:

#include <stdio.h>

#include <math.h>

int main() {

double num;

printf("Enter a number: ");

scanf("%lf", &num);

if (num >= 0) {

printf("Square root of %.2lf = %.2lf", num, sqrt(num));

} else {

printf("Square root of a negative number is not possible.");

}

return 0;

}

2\. Check if a Number is an Armstrong Number:

#include <stdio.h>

#include <math.h>

int isArmstrong(int number) {

int originalNumber, remainder, result = 0, n = 0;

originalNumber = number;

while (originalNumber != 0) {

originalNumber /= 10;

++n;

}

originalNumber = number;

while (originalNumber != 0) {

remainder = originalNumber % 10;

result += pow(remainder, n);

originalNumber /= 10;

}

return result == number;

}

int main() {

int number;

printf("Enter a number: ");

scanf("%d", &number);

if (isArmstrong(number)) {

printf("%d is an Armstrong number.", number);

} else {

printf("%d is not an Armstrong number.", number);

}

return 0;

}

3\. Convert Decimal to Octal:

#include <stdio.h>

void decimalToOctal(int decimalNumber) {

int octalNumber = 0, i = 1;

while (decimalNumber != 0) {

octalNumber += (decimalNumber % 8) * i;

decimalNumber /= 8;

i *= 10;

}

printf("Octal equivalent: %d", octalNumber);

}

int main() {

int decimalNumber;

printf("Enter a decimal number: ");

scanf("%d", &decimalNumber);

decimalToOctal(decimalNumber);

return 0;

}

4\. Find the Maximum and Minimum Element in an Array:

#include <stdio.h>

int main() {

int array[] = {4, 2, 6, 8, 1, 9};

int n = sizeof(array) / sizeof(array[0]);

int max = array[0];

int min = array[0];

for (int i = 1; i < n; i++) {

if (array[i] > max) {

max = array[i];

}

if (array[i] < min) {

min = array[i];

}

}

printf("Maximum element in array: %d\n", max);

printf("Minimum element in array: %d\n", min);

return 0;

}

5\. Check if a String is a Palindrome:

#include <stdio.h>

#include <string.h>

int isPalindrome(char str[]) {

int length = strlen(str);

for (int i = 0; i < length / 2; i++) {

if (str[i] != str[length - i - 1]) {

return 0;

}

}

return 1;

}

int main() {

char str[100];

printf("Enter a string: ");

scanf("%s", str);

if (isPalindrome(str)) {

printf("%s is a palindrome.", str);

} else {

printf("%s is not a palindrome.", str);

}

return 0;

}

SET-16

1\. Check if a Number is a Prime Number:

#include <stdio.h>

int isPrime(int num) {

if (num <= 1) {

return 0;

}

for (int i = 2; i * i <= num; i++) {

if (num % i == 0) {

return 0;

}

}

return 1;

}

int main() {

int num;

printf("Enter a positive integer: ");

scanf("%d", &num);

if (isPrime(num)) {

printf("%d is a prime number.", num);

} else {

printf("%d is not a prime number.", num);

}

return 0;

}

2\. Calculate the Factorial of a Number:

#include <stdio.h>

unsigned long long factorial(int n) {

if (n == 0) {

return 1;

} else {

return n * factorial(n - 1);

}

}

int main() {

int n;

printf("Enter a non-negative integer: ");

scanf("%d", &n);

printf("Factorial of %d = %llu", n, factorial(n));

return 0;

}

3\. Sort an Array using Insertion Sort:

#include <stdio.h>

void insertionSort(int arr[], int n) {

int i, key, j;

for (i = 1; i < n; i++) {

key = arr[i];

j = i - 1;

while (j >= 0 && arr[j] > key) {

arr[j + 1] = arr[j];

j = j - 1;

}

arr[j + 1] = key;

}

}

void printArray(int arr[], int n) {

for (int i = 0; i < n; i++) {

printf("%d ", arr[i]);

}

printf("\n");

}

int main() {

int arr[] = {12, 11, 13, 5, 6};

int n = sizeof(arr) / sizeof(arr[0]);

insertionSort(arr, n);

printf("Sorted array: \n");

printArray(arr, n);

return 0;

}

4\. Calculate the Sum of Natural Numbers using Recursion:

#include <stdio.h>

int sumOfNaturalNumbers(int n) {

if (n != 0) {

return n + sumOfNaturalNumbers(n - 1);

} else {

return n;

}

}

int main() {

int num;

printf("Enter a positive integer: ");

scanf("%d", &num);

printf("Sum of first %d natural numbers: %d", num, sumOfNaturalNumbers(num));

return 0;

}

5\. Calculate the Power of a Number using Recursion:

#include <stdio.h>

long long power(int base, int exponent) {

if (exponent != 0) {

return (base * power(base, exponent - 1));

} else {

return 1;

}

}

int main() {

int base, exponent;

printf("Enter base and exponent: ");

scanf("%d %d", &base, &exponent);

printf("%d^%d = %lld", base, exponent, power(base, exponent));

return 0;

}

SET-17

1\. Calculate the GCD and LCM of Two Numbers:

#include <stdio.h>

int gcd(int a, int b) {

if (b == 0) {

return a;

}

return gcd(b, a % b);

}

int lcm(int a, int b) {

return (a * b) / gcd(a, b);

}

int main() {

int num1, num2;

printf("Enter two positive integers: ");

scanf("%d %d", &num1, &num2);

printf("GCD of %d and %d is %d\n", num1, num2, gcd(num1, num2));

printf("LCM of %d and %d is %d", num1, num2, lcm(num1, num2));

return 0;

}

2\. Swap Two Numbers without Using a Third Variable:

#include <stdio.h>

int main() {

int num1, num2;

printf("Enter two numbers: ");

scanf("%d %d", &num1, &num2);

printf("Before swapping: a = %d, b = %d\n", num1, num2);

num1 = num1 + num2;

num2 = num1 - num2;

num1 = num1 - num2;

printf("After swapping: a = %d, b = %d", num1, num2);

return 0;

}

3\. Check if a Number is a Perfect Square:

#include <stdio.h>

int isPerfectSquare(int num) {

for (int i = 1; i * i <= num; i++) {

if (num == i * i) {

return 1;

}

}

return 0;

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isPerfectSquare(num)) {

printf("%d is a perfect square.", num);

} else {

printf("%d is not a perfect square.", num);

}

return 0;

}

4\. Calculate the Sum of Digits of a Number:

#include <stdio.h>

int sumOfDigits(int num) {

if (num == 0) {

return 0;

}

return (num % 10 + sumOfDigits(num / 10));

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

printf("Sum of digits of %d = %d", num, sumOfDigits(num));

return 0;

}

5\. Print the ASCII Value of Characters:

#include <stdio.h>

int main() {

char ch;

printf("Enter a character: ");

scanf(" %c", &ch);

printf("ASCII value of %c is %d", ch, ch);

return 0;

}

SET-18

1\. Calculate the Area of a Triangle:

#include <stdio.h>

int main() {

float base, height, area;

printf("Enter the base of the triangle: ");

scanf("%f", &base);

printf("Enter the height of the triangle: ");

scanf("%f", &height);

area = 0.5 * base * height;

printf("Area of the triangle = %.2f", area);

return 0;

}

2\. Check if a Number is a Palindrome:

#include <stdio.h>

int isPalindrome(int num) {

int reversedNum = 0, originalNum = num;

while (num != 0) {

reversedNum = reversedNum * 10 + num % 10;

num /= 10;

}

return reversedNum == originalNum;

}

int main() {

int num;

printf("Enter a number: ");

scanf("%d", &num);

if (isPalindrome(num)) {

printf("%d is a palindrome.", num);

} else {

printf("%d is not a palindrome.", num);

}

return 0;

}

3\. Check if a Year is a Leap Year:

#include <stdio.h>

int isLeapYear(int year) {

if (year % 400 == 0) {

return 1;

}

if (year % 100 == 0) {

return 0;

}

if (year % 4 == 0) {

return 1;

}

return 0;

}

int main() {

int year;

printf("Enter a year: ");

scanf("%d", &year);

if (isLeapYear(year)) {

printf("%d is a leap year.", year);

} else {

printf("%d is not a leap year.", year);

}

return 0;

}

4\. Calculate the Power Set of a Set (Recursive Approach):

#include <stdio.h>

#include <math.h>

void printPowerSet(char *set, int set_size) {

unsigned int pow_set_size = pow(2, set_size);

int counter, j;

for (counter = 0; counter < pow_set_size; counter++) {

for (j = 0; j < set_size; j++) {

if (counter & (1 << j))

printf("%c", set[j]);

}

printf("\n");

}

}

int main() {

char set[] = {'a', 'b', 'c'};

printPowerSet(set, 3);

return 0;

}

5\. Calculate the Mean and Standard Deviation of N Numbers:

#include <stdio.h>

#include <math.h>

int main() {

int n, i;

float num[100], sum = 0.0, mean, standardDeviation = 0.0;

printf("Enter the number of data: ");

scanf("%d", &n);

printf("Enter %d elements: ", n);

for (i = 0; i < n; ++i) {

scanf("%f", &num[i]);

sum += num[i];

}

mean = sum / n;

for (i = 0; i < n; ++i)

standardDeviation += pow(num[i] - mean, 2);

printf("Mean = %.2f\n", mean);

printf("Standard Deviation = %.2f", sqrt(standardDeviation / n));

return 0;

}

SET-19

1\. Calculate the Power of a Number:

#include <stdio.h>

long long power(int base, int exponent) {

long long result = 1;

while (exponent != 0) {

result *= base;

--exponent;

}

return result;

}

int main() {

int base, exponent;

printf("Enter the base number: ");

scanf("%d", &base);

printf("Enter the exponent: ");

scanf("%d", &exponent);

printf("%d raised to the power of %d is %lld", base, exponent, power(base, exponent));

return 0;

}

2\. Implement Bubble Sort:

#include <stdio.h>

void bubbleSort(int array[], int size) {

for (int step = 0; step < size - 1; ++step) {

for (int i = 0; i < size - step - 1; ++i) {

if (array[i] > array[i + 1]) {

// swap

int temp = array[i];

array[i] = array[i + 1];

array[i + 1] = temp;

}

}

}

}

int main() {

int data[] = {9, 5, 1, 4, 3};

int size = sizeof(data) / sizeof(data[0]);

bubbleSort(data, size);

printf("Sorted Array in Ascending Order:\n");

for (int i = 0; i < size; ++i) {

printf("%d  ", data[i]);

}

return 0;

}

3\. Implement Selection Sort:

#include <stdio.h>

void selectionSort(int array[], int size) {

for (int step = 0; step < size - 1; ++step) {

int min_idx = step;

for (int i = step + 1; i < size; ++i) {

if (array[i] < array[min_idx]) {

min_idx = i;

}

}

// Swap the found minimum element with the first element

int temp = array[min_idx];

array[min_idx] = array[step];

array[step] = temp;

}

}

int main() {

int data[] = {20, 12, 10, 15, 2};

int size = sizeof(data) / sizeof(data[0]);

selectionSort(data, size);

printf("Sorted array in ascending order:\n");

for (int i = 0; i < size; ++i) {

printf("%d ", data[i]);

}

return 0;

}

4\. Check if a String is a Substring of Another String:

#include <stdio.h>

#include <string.h>

int isSubstring(char str1[], char str2[]) {

if (strstr(str1, str2) != NULL) {

return 1;

}

return 0;

}

int main() {

char str1[100], str2[100];

printf("Enter the first string: ");

scanf("%s", str1);

printf("Enter the second string: ");

scanf("%s", str2);

if (isSubstring(str1, str2)) {

printf("%s is a substring of %s.", str2, str1);

} else {

printf("%s is not a substring of %s.", str2, str1);

}

return 0;

}

5\. Implement a Simple Calculator:

#include <stdio.h>

int main() {

char operator;

double num1, num2;

printf("Enter an operator (+, -, *, /): ");

scanf("%c", &operator);

printf("Enter two numbers: ");

scanf("%lf %lf", &num1, &num2);

switch (operator) {

case '+':

printf("%.1lf + %.1lf = %.1lf", num1, num2, num1 + num2);

break;

case '-':

printf("%.1lf - %.1lf = %.1lf", num1, num2, num1 - num2);

break;

case '*':

printf("%.1lf * %.1lf = %.1lf", num1, num2, num1 * num2);

break;

case '/':

if (num2 != 0) {

printf("%.1lf / %.1lf = %.1lf", num1, num2, num1 / num2);

} else {

printf("Error! Division by zero.");

}

break;

default:

printf("Error! Invalid operator.");

}

return 0;

}

SET-20

1\. Implement a Queue using an Array:

#include <stdio.h>

#define SIZE 5

int items[SIZE];

int front = -1, rear = -1;

int isFull() {

if (front == 0 && rear == SIZE - 1) {

return 1;

}

return 0;

}

int isEmpty() {

if (front == -1) {

return 1;

}

return 0;

}

void enQueue(int element) {

if (isFull()) {

printf("\nQueue is full");

} else {

if (front == -1) {

front = 0;

}

rear++;

items[rear] = element;

printf("\nInserted -> %d", element);

}

}

void deQueue() {

if (isEmpty()) {

printf("\nQueue is empty");

} else {

printf("\nDeleted -> %d", items[front]);

front++;

if (front > rear) {

front = rear = -1;

}

}

}

void display() {

int i;

if (isEmpty()) {

printf("\nQueue is empty");

} else {

printf("\nQueue elements are:\n");

for (i = front; i <= rear; i++) {

printf("%d  ", items[i]);

}

}

}

int main() {

// Queue operations

deQueue();

enQueue(1);

enQueue(2);

enQueue(3);

enQueue(4);

enQueue(5);

enQueue(6);

display();

// deQueue removes element entered first i.e. 1

deQueue();

// Now we have just 4 elements

display();

return 0;

}

2\. Calculate the Simple Interest:

#include <stdio.h>

int main() {

float principle, rate, time, simpleInterest;

printf("Enter principle amount: ");

scanf("%f", &principle);

printf("Enter rate of interest: ");

scanf("%f", &rate);

printf("Enter time in years: ");

scanf("%f", &time);

simpleInterest = (principle * rate * time) / 100;

printf("Simple Interest = %f", simpleInterest);

return 0;

}

3\. Calculate the Compound Interest:

#include <stdio.h>

#include <math.h>

int main() {

float principle, rate, time, compoundInterest;

printf("Enter principle amount: ");

scanf("%f", &principle);

printf("Enter rate of interest: ");

scanf("%f", &rate);

printf("Enter time in years: ");

scanf("%f", &time);

compoundInterest = principle * (pow((1 + rate / 100), time));

printf("Compound Interest = %f", compoundInterest);

return 0;

}

4\. Print the Fibonacci Series up to n terms:

#include <stdio.h>

void printFibonacci(int n) {

int a = 0, b = 1, c, i;

if (n <= 0)

return;

printf("%d ", a);

for (i = 2; i <= n; i++) {

printf("%d ", b);

c = a + b;

a = b;

b = c;

}

}

int main() {

int terms;

printf("Enter the number of terms: ");

scanf("%d", &terms);

printf("Fibonacci series up to %d terms: ", terms);

printFibonacci(terms);

return 0;

}

5\. Calculate the Factorial of a Number using Iteration:

#include <stdio.h>

unsigned long long factorial(unsigned int n) {

unsigned long long fact = 1;

for (int i = 1; i <= n; ++i) {

fact *= i;

}

return fact;

}

int main() {

int num;

printf("Enter a positive integer: ");

scanf("%d", &num);

printf("Factorial of %d = %llu", num, factorial(num));

return 0;

}