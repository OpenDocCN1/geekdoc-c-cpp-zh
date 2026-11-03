Since the conditional operator is right associative so this expression is considered as:

x ? y : (a ? b : c)

If x is non zero then the value of this expression will be equal to y. If x is zero then value of this expression will be equal to the value of expression (a ? b : c) i.e. equal to b if a is non zero and equa to c if a is zero.

# 4.14 Role Of Parentheses In Evaluating Expressions

If we want to change the order of precedence of any operation, we can use parentheses. Accordin to the parentheses rule, all the operations that are enclosed within parentheses are performed first.

For example in expression 24/2+4, division will take place before addition according to precedence rul but if we enclose 2+4 inside parentheses then addition will be performed first. So the value of expressio 24/(2+4) is 4.

For evaluation of expression inside parentheses same precedence and associativity rules apply. Fo example-

(22 - 4 ) / (2*4*2-1)

Here inside parentheses multiplication will be performed before addition.

There can be nesting of parentheses in expressions i.e. a pair of parentheses can be enclosed with another pair of parentheses. For example-

( 4* (3+2) )/10

In these cases, expressions within innermost parentheses are always evaluated first, and then ne innermost parentheses and so on, till outermost parentheses. After evaluation of all expressions wit parentheses, the remaining expression is evaluated as usual. In the above expression 3+2 is evaluat first and then 4*5 and then 20/10.

Sometimes in complex expressions, parentheses are used just to increase readability. For example comp the following two expressions-

x = a!=b && c*d>=m%n

x = (a!=b) && ( (c*d) >=(m%n) )

These two expressions are evaluated in the same way but the operations performed in second one clearer.

Let us take some expressions and evaluate them according the precedence, associativity and parenth rules.

a = 8, b = 4, c = 2, d = 1, e = 5 , f = 20

a + b - ( c + d ) * 3 % e + f / 9