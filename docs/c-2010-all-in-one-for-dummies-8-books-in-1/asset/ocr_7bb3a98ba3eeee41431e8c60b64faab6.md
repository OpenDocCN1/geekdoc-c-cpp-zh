# Skipping the Ref Statement 793

![](bbox=[0.218, 0.125, 0.858, 0.355])

Figure 3-1:
Deploying the PIAs in C# 3.0.

![](bbox=[0.218, 0.375, 0.858, 0.635])

Figure 3-2:
Deploying without
PIAs in C# 4.0.

Book VIII
Chapter 3

# Skipping the Ref Statement

Because of a different programming model, many COM APIs contain a lot of
reference parameters. Contrary to refs in C#, these are typically meant
to mutate a passed-in argument for the subsequent benefit of the caller but
are simply another way of passing value parameters.

Helping Out
with Interop