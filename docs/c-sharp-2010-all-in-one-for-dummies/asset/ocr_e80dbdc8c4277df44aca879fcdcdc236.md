# Chapter 2: Improving Productivity with Named and Optional Parameters

# In This Chapter

+   - Distinguishing between named and optional parameters
+   - Using optional parameters
+   - Implementing reference types
+   - Declaring Output parameters

Parameters, as you probably remember, are the inputs to methods. They are the values that you put in so that you get a return value. Sometimes, the return values are parameters, too, which confuses things.

In the world of C# and most C-derived languages, parameters can't be optional. Instead of making parameters optional, you are just expected to make a separate overload for every version of the method that you expect your users to need.

This pattern works fairly well, but there are still a lot of problems. Many VB programmers point to the flexible parameterization as a strong reason to use VB over C#.

C# 4.0 has optional parameters. Optional parameters are parameters that have a default value right in the method signature — just like the VB.NET implementation. This is one more step toward language parity, and again in the name of COM programming.

It's the same control versus productivity issue that Chapter 1 shows us about the dynamic type. Optional parameters give you just enough rope to hang yourself. A programmer can make mistakes just as easily as he can help himself.