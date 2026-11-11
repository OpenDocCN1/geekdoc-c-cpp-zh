# # Getting into the Algo-rhythm

![](bbox=[0.78, 0.02, 0.96, 0.2])

Computers do things fast – a computer that costs £5 can have a clock speed of 1GHz, meaning it does one *billion* things every second. So most of the time you won't need to worry about how quickly your program runs. Sometimes, though, you may find a program takes a long time to complete. That's when you need to worry about the algorithms you are using.

An algorithm is just the way your code is solving a particular task – such as sorting a list into alphabetical order. There's usually lots of ways to write code to complete a task, and each has its own complexity – that's how the time it takes to run changes as you increase the amount of data.

# ## How complex is your code?

An algorithm with complexity O(n) is called linear – that means if you double the size of your data set (n) it takes twice as long to run. But another algorithm for the same task might have complexity O(n²) – now when you double the amount of data the algorithm takes four times as long to run. When n is small the time differences don't matter, but if you're working with millions of elements the second algorithm can take tens of thousands of times longer than the first to solve the same task!

> > It can be tempting to try and find the fastest algorithm for everything in your code, but it's not always the best idea. You'll not only spend a lot of time and effort to make your code run a lot faster, but the code you'll end up with will be harder to understand or change. Spending a lot of time speeding up code that doesn't need it is called premature optimisation. You should only worry about your code's speed if it's causing you problems.

There are lots of other possible complexities – the smaller the value inside the bracket comes to for a value of n, the faster the algorithm will run on large sets of data. To work out the complexity of your own algorithms take a look at the code and try to work out how many times it will need to run for n pieces of data. Nested loops (loops inside other loops) are a sign that your algorithm may have a high complexity. Consider if there's a way to rewrite it to avoid these if you're planning to deal with lots of data.