Let us take some expressions and see how they will be evaluated-

(i) x = a+b < c

Here + operator has higher precedence than < and =, and < has more precedence than =, so first a+b will be evaluated, then < operator will be evaluated, and at last the whole value will be assigned to x. If initial values are a = 2, b = 6, c = 9, then final value of x will be 1.

(ii) x *= a + b

Here + operator has higher precedence than *=, so a+b will be evaluated before compound assignment. This is interpreted as x = x*(a+b) and not as x = x*a+b. If initial values are x = 5, a = 2, b = 6, then final value of x will be 13.

(iii) x = a<=b || b==c

Here order of evaluation of operators will be <=, ==, ||. If initial values are a = 2, b = 3, c = 4, then final value of x will be 1.

In the above examples we have considered expressions that contain operators having different precedence levels. Now consider a situation when two operators with the same precedence occur in an expression.

For example-

5 + 16 / 2 * 4

Here / and * have higher precedence than + operator, so they will be evaluated before addition. But / and * have same precedence, so which one of them will be evaluated first still remains a problem. If / is evaluated before *, then the result is 37 otherwise the result is 7. Similarly consider this expression-

20 - 7 - 5 - 2 -1

Here we have four subtraction operators, which of course have the same precedence level. If we decide to evaluate from right to left answer will be 5, and if we evaluate from left to right the answer will be 17.

To solve these types of problems, an associativity property is assigned to each operator. Associativity of the operators within same group is same. All the operators either associate from left to right or from right to left. The associativity of all operators is also given in the precedence table. Now again consider the above two expressions-

5 + 16 / 2 *4

Since / and * operators associate from left to right so / will be evaluated before * and the correct result is 37.

20 - 7 - 5 - 2 -1

The subtraction operator associates from left to right so the value of this expression is 5.

The assignment operator associates from right to left. Suppose we have a multiple assignment expression like this-

x = y = z = 5

Here initially the integer value 5 is assigned to variable z and then value of expression z = 5 is assigned to variable y. The value of expression z = 5 is 5, so 5 is assigned to variable y and now the value of expression y = z = 5 becomes 5. Now value of this expression is assigned to x and the value of whole expression x = y = z = 5 becomes 5.

The conditional operator also associates form right to left. Consider this expression-

x ? y : a ? b : c