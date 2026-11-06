# MyThis and MyThat

As you progress through your computer programming life (which is, we hope, in addition to your life as a millionaire), you are likely to notice that, for some reason, some computer programmers seem to favor variable names that start with the word *My*. Other computer programmers despise this practice and completely distance themselves from it. We have seen such computer identifiers as MyClass, MyNumber, MyHeight, MyName, MyCar, MyWhatASurprise, MyLar, MyStro, and MyOpic. Personally, we have no problem using names that start with *My*, especially in training exercises.

![](bbox=[0.143, 0.362, 0.229, 0.435])

Although most C++ code is in lowercase, you are free to use uppercase letters in your variable names. However, C++ distinguishes between the two. Therefore, if you have a variable called count, you cannot access it later in your application by calling it Count with a capital C. The compiler treats the two names as two different variables, which makes C++ case sensitive. But on the other hand, please don’t use two separate variables in the same application — one called count and one called Count. Although the compiler doesn’t mind, the mere humans that may have to read your code or work on it later might get confused.

Here are the rules you need to follow when creating a variable name:

+   - **Characters:** You can use any uppercase letter, lowercase letter, number, or underscore in your variable names. Other symbols (such as spaces or the ones above the number keys on your keyboard) are not allowed in variable names. The only catches are that:
+     - The first character *cannot* be a number.
+     - The variable name *cannot* consist of only numbers.
+   - **Length:** Most compilers these days allow you to have as many characters in the variable name as you want. Just to be sure, and to prove we’re easily amused, in Code::Blocks we successfully created a variable with a name that was over 1,000 characters in length. However, we wouldn’t want to have to type that thing over and over. Instead, we recommend keeping variable names long enough to make sense but short enough that you can type them easily. Most people prefer anywhere from five to ten characters or so.

Examples of acceptable variable names are Count, current_name, address_1000, and LookupAmount. Table 3-2 lists some variable names that are not allowed.