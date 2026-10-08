If the user enters the numbers 5, 8, 9, and -1, how many times will the condition in the following algorithm be evaluated?

+   1. enter number
2. repeat
display number
enter number
end repeat while (number is greater than equal to 0)

If the user enters the numbers 0 and -4, how many times will the condition in Question 3's algorithm be evaluated?

# The while Statement

C++ provides the while statement for coding a postfix loop. The statement's syntax is in Figure 8-7. As the bolded text in the syntax indicates, essential components of the statement include the do and while keywords, the parentheses that surround the condition, the braces, and the semicolon. The italicized items indicate where the programmer must supply information. In this case, the programmer must supply the condition, which must be phrased as a loop condition. As the while statement, the condition in the while statement must evaluate to true or false. The condition can contain variables, constants, functions, arithmetic operators, comparison operators, and logical operators. Besides it provides the statements to be processed when the condition evaluates to true. Although not required, some programmers use a comment (such as //begin loop) to mark the beginning of the while statement, because it makes easier to read and understand. Also included in Figure 8-7 are examples of using the while statement. The while clause in Example 1 tells the computer to repeat the loop body instructions as long as the age variable is greater than zero. The loop will stop when the second number entered by the user is zero or a negative number. The while clause in Example 2 indicates that the loop instructions should be repeated as long as the value in the makeEntry variable is either the uppercase Y or the lowercase y. In this case, the loop will stop when the user's second entry is anything other than the letter Y entered in either uppercase or lowercase. You could also write the last line in the loop as } while (touppermakeEntry) == 'Y'; or while (tolowermakeEntry) == 'y';

> Recall that a looping condition specifies the requirement for processing the loop body.