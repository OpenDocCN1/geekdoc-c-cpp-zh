
### Figure 5-22: Method to display results

```
private void DisplayResults(float rateResting, float age, float rateTraining)
{
    // Display Results
    lstResults.Items.Add(string.Format("{0,20}{1,10}", "Resting Heart Rate:", rateResting));
    lstResults.Items.Add(string.Format("{0,20}{1,10}", "Age:", age));
    lstResults.Items.Add(string.Format("{0,20}{1,10}", "Training Heart Rate:",
        rateTraining.ToString("N0")));
}
```

The following statement calls this method, as shown in Figure 5-20, passing the three arguments by value.

```
DisplayResults(restingHeartRate, age, trainingHeartRate);
```

Note that resting heart rate and training heart rate are represented by the parameters rateResting and rateTraining, which are different from the names of the corresponding variables in the calling program. This is just to show that the name of an argument and the corresponding parameter may be different.

### Getting the Big Picture

An advantage of the top-down design is that the code in the calling program, btnTrainingRate_Click, primarily consists of three statements to call the three methods, as shown in Figure 5-20. Thus, it is easier to get a high level view of the application by looking at the code in the calling program. In addition, the methods corresponding to the subtasks are more reusable, compared to having all code in a single program.

Now you can create a new form that implements the top-down design.

### Step 1-21: Create a new form named HeartRateTopDown. Copy the controls from the form HeartRate.

This form has the same controls as the form HeartRate. HeartRateTopDown should look as follows:

![](img/143bad48262566137acc9c41f668a88f_179_0.png)

### Step 1-22: Create the method GetPersonalData (see Figure 5-19).

Add the statements within btnTrainingRate_Click event handler to call GetPersonalData (see Figure 5-20).

### Step 1-23: Create the method ComputeTrainingRate (see Figure 5-21).

Add the statements within btnTrainingRate_Click event handler to call ComputeTrainingRate (see Figure 5-20).

### Step 1-24: Create the method DisplayResults.

Add the statements within btnTrainingRate_Click event handler to call DisplayResults (see Figure 5-20).

### Step 1-25: Put breaks in the calling program at each call statement.

Run the form. Verify that the values assigned to restingRate and age in GetPersonalData changes the values of the corresponding arguments in the calling program. Similarly, verify that assigning the computed value to restingRate in the ComputeTrainingRate changes the value of restingHeartRate in the calling program.

The complete code for the HeartRateTopDown form looks as follows:

```
19  private void GetPersonalData(ref float restingRate, ref float age)
20  {
21      // Get resting rate and age from Textboxes:
22      restingRate = float.Parse(txtRestingRate.Text);
23      age = float.Parse(txtAge.Text);
24  }
25
26  private void ComputeTrainingRate(float restingRate, float age, ref float trainingRate)
27  {
28      float maximumRate;    //trainingRate is not declared here; it is a parameter
29      // Compute maximum heart rate:
30      maximumRate = 220 - age;
31      // Compute training heart rate
32      trainingRate = 0.6F * (maximumRate - restingRate) + restingRate;
33  }
34
35  private void DisplayResults(float rateResting, float age, float rateTraining)
36  {
37      // Display Results
38      lstResults.Items.Add(string.Format("{0,20}{1,10}", "Resting Heart Rate:", rateResting));
39      lstResults.Items.Add(string.Format("{0,20}{1,10}", "Age:", age));
40      lstResults.Items.Add(string.Format("{0,20}{1,10}", "Training Heart Rate:",
41                                  rateTraining.ToString("N0")));
42  }
43
44  private void btnTrainingRate_Click(object sender, EventArgs e)
45  {
46      // Call GetPersonalData
47      float restingHeartRate = 0, age = 0;
48      GetPersonalData(ref restingHeartRate, ref age);
49
50      // Call ComputeTrainingRate
51      float trainingHeartRate = 0;
52      ComputeTrainingRate(restingHeartRate, age, ref trainingHeartRate);
53
54      // Call DisplayResults
55      DisplayResults(restingHeartRate, age, trainingHeartRate);
56  }
```

### It’s time to practice!

Modify ComputeTrainingRate, DisplayResults and the call statements as follows:

ComputeTrainingRate returns maximumRate to the calling program, in addition to trainingRate. Pass the maximumRate to DisplayResults as shown in the following structure chart. Display the maximumRate along with the trainingRate.

![](img/143bad48262566137acc9c41f668a88f_181_0.png)

### An Undesirable Design Using Noncohesive Methods

In the top-down design shown in Figure 5-18, the task of computing the training heart rate is broken down to three subtasks represented by the methods GetPersonalData, ComputeTrainingRate and DisplayResults. These methods are called in sequence by a main program (the Click event procedure, btnTrainingRate_Click). Data is shared between the calling program and the called program through parameters. As discussed earlier in this chapter, such a design makes the methods cohesive and reusable.

An alternate undesirable design that involves less reusable noncohesive methods is shown in Figure 5-23.

### Figure 5-23: Alternate undesirable design involving noncohesive methods

![](img/143bad48262566137acc9c41f668a88f_181_1.png)

In this design, the main program (the Click event procedure, btnTrainingRate_Click) calls the method GetPersonalData as in the top-down design.

However, the method GetPersonalData gets personal data, and instead of passing the data to the main program, it calls ComputeTrainingRate, passing restingRate and age to the method.

ComputeTrainingRate computes the training rate and then calls DisplayResults passing restingRate, age and trainingRate to the method.

DisplayResults displays the results as in the top-down design.

The above design suffers from several problems:

- 1. The methods GetPersonalData and ComputeTrainingRate are not cohesive. For example, ComputeTrainingRate doesn’t do a single well-defined task. It computes training rate and also displays results by calling DisplayResults. Similarly, GetPersonalData gets restingRate and age and also computes results by calling ComputeTrainingRate.
- 2. The methods GetPersonalData and ComputeTrainingRate are less reusable. For example, ComputeTrainingRate does more than computing the results, and it doesn’t return the result to the calling program.
- 3. It might be necessary to pass certain data to a method where it is not needed. For example, if the personal data includes the person’s name, the only way it can be passed to DisplayResults is by first passing it to ComputeTrainingRate, where it is not needed. Passing data to a method where it is not needed makes maintenance of code difficult.

### Review Questions

- 5.17 What is top-down design?
- 5.18 Describe two benefits of top-down design.

### 5.6 Methods That Return a Value

The methods we discussed in this chapter return values to the calling program only through parameters. Parameters allow any number of values to be returned.

The method itself can return a single value to the calling program, other than through parameters. An advantage of such a method is that the method can be used as a part of an expression. Figure 5-24 shows such a method, called TrainingRate, that computes training rate and returns it to the calling program:

### Figure 5-24: Value returning method, TrainingRate

```
private float TrainingRate(float restingRate, float age)
{
    float maximumRate;
    // Compute maximum heart rate:
    maximumRate = 220 - age;
    // Compute training heart rate and return it
    return 0.6F * (maximumRate - restingRate) + restingRate;
}
```

Here are the key differences between this method and the method ComputeTrainingRate that you developed earlier:

The header, `private float TrainingRate(float restingRate, float age)` shows no parameter to return the trainingRate. Then how is the trainingRate returned?

The method itself takes the place of a parameter and returns the value specified in the return statement, `return 0.6F * (maximumRate - restingRate) + restingRate;`

Because the method returns a value, the type of value returned, called return type, is specified in the header using the key word float instead of void. Further, the name of the method indicates the value returned by the method, not what the method does.

### Calling a Value Returning Method

This is how you call the method:

```
float trainingHeartRate = TrainingRate(restingHeartRate, age);
```

The value returned by TrainingRate is assigned to the float type variable, trainingHeartRate.

Next, we will develop a new form named HeartRateTopDownAlt, with an alternate version of ComputeTrainingRate that does not use a parameter to return training rate. This form has the same user interface as HeartRateTopDown, as shown in the following figure:
