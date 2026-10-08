# # Adding a Variable

The output message will be generated in two steps. First, the message part is composed before executing the WriteLine activity. Second, the timestamp is added. Workflow variables are the constructs you use to store values and use them within the workflow. You can take a workflow variable for an account just like a local method variable for the declaring method.

Select the "Hello World" sequence, click the Variables link in the design surface, and add a new variable. Name it temp and leave its type as String. The Scope of the variable will be set to "Hello Workflow," Figure 11-7 shows how the Variables pane look after adding temp.

| Name | VariableType | Scope | Default |
|---|---|---|--|
| temp | String | Hello Workflow | |

**FIGURE 11-7:** Define the temp variable

# # Creating the Output Value

Add an Assign activity (found in the Primitives category) between the first and second WriteLine activity. On the design surface, it displays two boxes—the first one names the variable to store the expression represented by the second. In the property window, these boxes are covered by the To and Value properties, respectively.

Set the first box (To property to temp) and the second one (Value property) to "Message: " + Message. The value of temp contains the message the second WriteLine activity is about to display, so set its property to temp. Add another Assign activity between the second and third WriteLine and set the To and Value properties to temp and temp = "" + DateTime.Now.ToString("HH:mm:ss") + "",).

Add third Assign activity after the third WriteLine and set it to assign the value of temp to the Result output. The workflow would look like the design surface in Figure 11-8.

![](bbox=[0.675, 0.275, 0.875, 0.73])

**FIGURE 11-8:** The modified workflow

# # Extracting the Workflow Output

This workflow produces the output you need, but how should it be extracted from the workflow. Modify the Main method in the Program.cs file as shown in Listing 11-2.

**LISTING 11-2:** The Modified Program.cs file (HelloWorkflow)

```
using System;
using System.Collections.Generic;
using System.Activities;

namespace HelloWorkflow
{
    * 
```

![](bbox=[0.035, 0.89, 0.095, 0.935])