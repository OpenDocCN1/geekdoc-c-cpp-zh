Notice: Please note that when a constant is declared, the equals symbol ( = ) is used instead of the left arrow.

This last solution is the best choice for many reasons.

+   > No one, including the programmer, can change the value of VAT just by accidentally writing a statement such as VAT ← 0.60 in any position of the program.
+   > The potential for typographical errors is minimized.
+   > The number of multiplication and division operations is kept as low as possible.
+   > If one day the finance minister decides to increase the Value Added Tax from 20% to 22%, the programmer needs to change just one line of code!

# 5.3 How Many Types of Variables and Constants Exist in PHP?

Many different types of variables and constants exist in all computer languages. The reason for this diversity is the different types of data each variable or constant can hold. Most of the time, variables and constants hold the following types of data.

+   > **Integers**: Integer values are positive or negative numbers without any fractional part, such as 5, 100, 135, -25, and -5123.
+   > **Reals**: Real values are positive or negative numbers that include a fractional part, such as 5.14, 7.23, 5.0, 3.14, and -23.78976. Real values are also known as "floats."
+   > **Booleans**¹: Boolean variables or constants can hold only one of two values: true or false.
+   > **Characters**: Characters are alphanumeric values (always enclosed in single or double quotes) such as "Hello Zeus", 'I am 25 years old', or 'Peter Loves Jane For Ever'. Character values are also known as "strings"!!! (Probably the word "string" makes you visualize something wearable, but unfortunately it's not. Please keep your dirty precious mind focused on computer science!)

# 5.4 Rules for Naming Variables in PHP

Certain rules must be followed when assigning names to your variables.

+   > PHP variables are written as $var_name, where var_name is the name of the variable. The name can contain only Latin characters (English uppercase or lowercase characters), numbers, and the underscore character ( _ ). Examples of variable names are $firstName, $last_name1, and $age.
+   > Variable names are case sensitive, which means there is a distinct difference between uppercase and lowercase characters. For example, $myVAR, $myvar, $MYVAR, and $MyVar are actually four different variables.