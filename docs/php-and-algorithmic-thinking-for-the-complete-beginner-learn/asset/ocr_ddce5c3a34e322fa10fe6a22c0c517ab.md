Consider an algorithm that lets the user enter the prices of three different products and then calculates and displays the 20% Value Added Tax (known as VAT) for each product. The flowchart in Figure 5-1 shows this process when no constant is used.

![](bbox=[0.28, 0.18, 0.72, 0.62])

Figure 5-1 Calculating the 20% VAT for three products without the use of a constant

Even though this algorithm is absolutely correct, the problem is that the author used the 20% VAT (20/100) three times. If this were an actual computer program, the CPU would be forced to calculate the result of the division (20/100) three individual times.

> Notice: Generally speaking, division and multiplication are time consuming operations that must be avoided when possible.

A much better solution would be to use a variable, as shown in Figure 5-2. This reduces the number of division and multiplication operations and also decreases the potential for typographical errors.