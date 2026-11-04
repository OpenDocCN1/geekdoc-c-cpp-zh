For example, suppose that you select the try code snippet. The following block of code will be inserted automatically:

```
private void Form1_Load(object sender, EventArgs e)
{
    try
    {
    }
    catch (Exception)
    {
        throw;
    }
}
```

You can also use the Surround With code snippets feature. Suppose that you have the following statements:

```
private void Form1_Load(object sender, EventArgs e)
{
    int num1 = 5;
    int num2 = 0;
    int result = num1 / num2;
}
```

The third statement is dangerous because it could result in a division-by-zero runtime error, so it would be good to wrap the code in a try-catch block. To do so, you can highlight the block of code you want to put within a try-catch block and right-click it. Select Surround With (see Figure 2-40), and then select the try code snippet.

![](bbox=[0.35, 0.8, 0.65, 0.93])

Figure 2-40