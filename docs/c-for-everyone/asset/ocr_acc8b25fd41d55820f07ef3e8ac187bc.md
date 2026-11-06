> Never point an arrow inside another branch.

There is one issue that you need to be aware of when drawing flowcharts. Unconstrained branching and merging can lead to “spaghetti code”, a messy network of possible pathways through a program.
There is a simple rule for avoiding spaghetti code: Never point an arrow inside another branch.
To understand the rule, consider this example: Shipping costs are $5 inside the United States, except that to Hawaii and Alaska they are $10. International shipping costs are also $10. You might start with a flowchart like the following:

![](bbox=[0.679, 0.091, 0.89, 0.252])

![](bbox=[0.323, 0.289, 0.81, 0.579])

Now you may be tempted to reuse the “shipping cost = $10” task:

![](bbox=[0.323, 0.632, 0.81, 0.923])