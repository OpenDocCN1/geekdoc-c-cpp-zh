# Animating with the Expression Controller and Wiring Parameters

Expressions are looks that you make in the mirror when you're trying to wake up, but in Max they are a series of equations that define how an object acts. Max expressions can be as simple as adding two numbers together or as complex as several lines of MAXScript. But expressions enable you to create customized animated reactions.

Although Max expressions can be used with any Max spinner, they are mainly used within MAXScript scripts or in the Expression controller. The Expression controller is a specialized controller that lets you control the object's behavior using scripted expressions.

This chapter then looks at a unique way to drive animations based on object parameters. Parameters of one object can be wired to parameters of another object so that when one parameter changes, the wired parameter changes with it. For example, you can wire the On/Off parameter of a light to the movement of a switch. All parameters that can be animated can be wired.

As long as you are working with parameters, Max includes several helpful tools for viewing and working with the available parameters including the Parameter Collector. If the Parameter Collector doesn't gather the exact parameters that you need, you can create your own custom parameters also.

# IN THIS CHAPTER

+   - Using the Numerical Expression Evaluator
+   - Understanding the Expression controller interface
+   - Learning about operators, variables, and functions
+   - Wiring parameters with manipulator helpers
+   - Collecting parameters
+   - Creating custom parameters

# Working with Expressions in Spinners

Although much of this chapter focuses on using the Expression controller, the Expression Controller Interface isn't the only place where you can play with expressions. Expressions can also be entered into spinner controls using the Numerical Expression Evaluator, shown in Figure 35.1. This simple dialog box is accessed by selecting a spinner and pressing Ctrl+N.

# Cross-Ref

Another place that commonly uses expressions is the Parameter Wiring dialog box, which is covered later in this chapter.