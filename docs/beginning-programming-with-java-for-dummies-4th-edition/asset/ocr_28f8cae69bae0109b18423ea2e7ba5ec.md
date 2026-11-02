If you do the arithmetic by hand, the value you get for 9.0 / 5.0 * 21 + 32.0 is exactly 69.8. So run the code in Listing 8-5 and give celsius the value 21. You should get true when you display the value of fahrenheit == 69.8, right?

Well, no. Take a look at the run in Figure 8-12. When the computer evaluates fahrenheit == 69.8, the value turns out to be false, not true. What's going on here?

# Figure 8-12:
A run of the code in Listing 8-5.

![](bbox=[0.28, 0.38, 0.55, 0.48])

![](bbox=[0.15, 0.55, 0.22, 0.68])

Grouping separators vary from one country to another. The run shown in Figure 8-12 works almost everywhere in the world. But if the Celsius temperature is twenty-one-and-a-half degrees, you type 21.5 (with a dot) in some countries and 21,5 (with a comma) in others. Your computer's hardware doesn't have a built-in "country-ometer," but when you install the computer's operating system, you tell it what country you live in. Java programs access this information and use it to customize the way the nextDouble method works.

A little detective work can go a long way. So review the facts:

+   - Fact: The value of fahrenheit should be exactly 69.8.
+   - Fact: If fahrenheit is 69.8, then fahrenheit == 69.8 is true.
+   - Fact: In Figure 8-12, the computer displays the word false. So the expression fahrenheit == 69.8 isn't true.

How do you reconcile these facts? There can be little doubt that fahrenheit == 69.8 is false, so what does that say about the value of fahrenheit? Nowhere in Listing 8-5 is the value of fahrenheit displayed. Could that be the problem?

At this point, I use a popular programmer's trick. I add statements to display the value of fahrenheit.

```
fahrenheit = 9.0 / 5.0 * celsius + 32.0;
System.out.print("fahrenheit: ");   //Added
System.out.println(fahrenheit);     //Added
```