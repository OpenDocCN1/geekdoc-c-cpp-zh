
Figure 5-16 shows the updated calling program. The call statement now includes `trainingHeartRate` as an argument (line 60).

**Figure 5-16: Updated calling program**

```
50
51    private void btnTrainingRate_Click(object sender, EventArgs e)
52    {
53        float restingHeartRate, age;
54        // Get resting rate and age from Textboxes:
55        restingHeartRate = float.Parse(txtRestingRate.Text);
56        age = float.Parse(txtAge.Text);
57
58        // Call ComputeTrainingRate
59        float trainingHeartRate = 0;
60        ComputeTrainingRate(restingHeartRate, age, ref trainingHeartRate);
61        // Display training rate
62        lstResults.Items.Add(string.Format("{0,20}{1,10}", "Training Heart Rate:",
63                                    trainingHeartRate.ToString("N0")));
64    }
```

The keyword `ref` in the calling statement in line 60 specifies that the parameter is a reference type. Note that the name of the argument (`trainingHeartRate`) is different from the name of the parameter (`trainingRate`).

An argument passed by reference must be declared in the calling program, and it must be set to a value. The argument `trainingHeartRate` is declared and it is set to zero.

What happens when `ComputeTrainingRate` is called?

First, the reference to `trainingHeartRate` is passed to the parameter `trainingRate`. That means `trainingRate` will take the value of the argument `trainingHeartRate`.

Next, the method assigns the computed value to the parameter `trainingRate`. Because both the argument and the parameter share the same memory location, the computed value also is available to the argument `trainingHeartRate`.

Thus, passing by reference makes sharing between the calling program and the called program like a two-way street, as shown, whereas passing by value is like a one-way street.

```
ComputeTrainingRate(restingHeartRate, age, ref trainingHeartRate);

private void ComputeTrainingRate(float restingRate, float age, ref float trainingRate)
```

### Step 1-20: Update ComputeTrainingRate to include the parameter trainingRate, as shown in Figure 5-15.

Put breakpoints at the beginning and ending braces within the called method.

Make changes in the calling program, as shown in Figure 5-16.

Run the form. At the first breakpoint inside `ComputeTrainingRate`, observe that the parameter `trainingRate` has the value 0 (same as the value of the argument `trainingHeartRate`). At the second breakpoint at the end of the method, `trainingRate` has the computed value.

## 1 白鹭

![](img/143bad48262566137acc9c41f668a88f_174_0.png)

白鹭是一首精巧的诗。色素的配合，身段的大小，一切都很适宜。

白鹤太大而嫌生硬，即使如粉红的朱鹭或灰色的苍鹭，也觉得大了一些，而且太不寻常了。

然而白鹭却因为它的常见，而被人忘却了它的美。

那雪白的蓑毛，那全身的流线型结构，那铁色的长喙，那青色的脚，增之一分则嫌长，减之一分则嫌短，素之一忽则嫌白，黛之一忽则嫌黑。

在清水田里，时有一只两只白鹭站着钓鱼，整个的田便成了一幅嵌在玻璃框里的画。田的大小好像是有心人为白鹭设计的镜匣。

晴天的清晨，每每看见它孤独地站立于小树的绝顶，看来像是不安稳，而它却很悠然。这是别的鸟很难表现的一种嗜好。人们说它是在望哨，可它真是在望哨吗？

黄昏的空中偶见白鹭的低飞，更是乡居生活中的一种恩惠。那是清澄的形象化，而且具有生命了。

或许有人会感到美中不足，白鹭不会唱歌。但是白鹭本身不就是一首很优美的歌吗？

——不，歌未免太铿锵了。

白鹭实在是一首诗，一首韵在骨子里的散文诗。

## Review Questions

5.14 What is meant by passing an argument by reference?

5.15 The following code shows a method named ComputeSum, and the Click event handler of a button that calls the method:

```
private void btnExamScore_Click(object sender, EventArgs e)
{
    int exam1 = 150, exam2 = 100, total = 0;
    ComputeSum(exam1, exam2, ref total);
    lstDisplay.Items.Add(exam1 + " " + exam2 + " " + total);
}

private void ComputeSum(int exam1, int exam2, ref int sum)
{
    sum = exam1 + exam2;
    exam1 = 0;
    exam2 = 0;
}
```

What would be the output displayed in the ListBox when you click the button?

5.16 The following code shows a method named ComputeSum, and the Click event handler of a button that calls the method (note that the parameters are declared differently from the previous question):

```
private void btnExamScore_Click(object sender, EventArgs e)
{
    int exam1 = 10, exam2 = 15, total = 0;
    ComputeSum(ref exam1, ref exam2, ref total);
    lstDisplay.Items.Add(exam1 + " " + exam2 + " " + total);
}

private void ComputeSum(ref int test1, ref int test2, ref int sum)
{
    sum = test1 + test2;
    test1 = 0;
    test2 = 0;
}
```

What would be the output displayed in the ListBox when you run the Click event handler?

## 5.5 Top-Down Design

Top-down design involves breaking down a larger problem to smaller subtasks, each performed by a separate method, to make software development simpler and easier.

Though the task of computing the training heart rate is fairly simple, for the purpose of illustrating top-down design, let’s look at the subtasks of this problem. Figure 5-17 shows the code that you developed in Tutorial 1, with a couple of additional statements to display the resting rate and age, along with the training rate. This event handler calls the `ComputeTrainingRate` method to compute the training heart rate.

**Figure 5-17: Revised code to compute training rate**

```
private void btnTrainingRate_Click(object sender, EventArgs e)
{
    float restingHeartRate, age;

    // Get personal data (resting rate and age) from Textboxes:
    restingHeartRate = float.Parse(txtRestingRate.Text);
    age = float.Parse(txtAge.Text);

    // Call ComputeTrainingRate
    float trainingHeartRate = 0;
    ComputeTrainingRate(restingHeartRate, age, ref trainingHeartRate);

    // Display training rate
    lstResults.Items.Add(string.Format("{0,20}{1,10}", "Resting Heart Rate:", restingHeartRate));
    lstResults.Items.Add(string.Format("{0,20}{1,10}", "Age:", age));
    lstResults.Items.Add(string.Format("{0,20}{1,10}", "Training Heart Rate:", trainingHeartRate.ToString("N0")));
}
```

The task performed in this program can be broken down to three subtasks:

- 1. Get personal data.
- 2. Compute training rate.
- 3. Display results.

You already developed a method for the second subtask (compute the training rate). Now, you will develop two additional methods corresponding to the subtasks (get personal data and display results) and call all three methods from the `btnTrainingRate_Click` event handler, as represented in Figure 5-18.

Note that the resting heart rate is represented by the variable `restingHeartRate` in the calling program, but the corresponding parameter in `GetPersonalData` is called `restingRate`.

### Passing by reference versus class level variables

The `GetPersonalData` method illustrates how multiple values (`restingHeartRate` and `age`) may be passed from the called method to the calling method using reference parameters. An alternate way to share data between the two methods is to declare the variables `restingHeartRate` and `age` at the class level, and not specify any parameters for the `GetPersonalData` method. It should be noted that the values of such class level variables can be inadvertently changed by any method like `ComputeTrainingRate`.

### out parameter instead of ref parameter

Because data is to be passed from `GetPersonalData` to the calling program, and not from the calling program to `GetPersonalData`, `out` arguments may be used in place of `ref` arguments, as shown in the following statement:

```
private void GetPersonalData(out float restingRate, out float age)
```

In this case, the arguments in the calling program do not have to be initialized, and the keyword `ref` is replaced by `out` in the call statement:

```
float restingHeartRate, age;
GetPersonalData(out restingHeartRate, out age);
```

### Method to Compute Training Rate

You already developed the method to compute training rate in Tutorial 1. Figure 5-21 shows the method.

**Figure 5-21: ComputeTrainingRate method**

```
private void ComputeTrainingRate(float restingRate, float age, ref float trainingRate)
{
    float maximumRate; // trainingRate is not declared here; it is a parameter
    // Compute maximum heart rate:
    maximumRate = 220 - age;
    // Compute training heart rate
    trainingRate = 0.6F * (maximumRate - restingRate) + restingRate;
}
```

Figure 5-20 shows the statement that calls this method.

### Method to Display Results

Data need to be passed from the calling program to the `DisplayResults` method, but not the other way around. So, the resting rate, age, and training rate are passed by value to this method, as shown in Figure 5-22.
