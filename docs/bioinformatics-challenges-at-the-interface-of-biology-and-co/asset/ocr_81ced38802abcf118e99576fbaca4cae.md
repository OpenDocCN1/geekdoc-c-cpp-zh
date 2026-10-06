# # Chapter 6

# ## Algorithms and complexity

# ### 6.1 Overview

In this chapter, we begin to consider how computers have been brought to bear on some of the issues we've been discussing so far. We look at how to go about trying to solve problems algorithmically (from a more conceptual perspective of what computation is capable of and), and learn that computation has some surprising limits. From there, we consider how the reality of modern computer technology affects our ability to solve problems, and, conversely, how the problems faced by bioinformaticians may not be as amenable to solution as we expect. We'll also explore the methods available for ameliorating these shortcomings.

We're particularly concerned here with grasping concepts, so don't be put off by the minutiae—you don't need to remember or follow every algorithm in detail. By the end of the chapter, you should have gained an understanding of how bioinformatics problems require highly complex solutions if they're to provide the answers we seek, and why, given the computers we have at our disposal today, some problems may not be solvable without employing computer science techniques.

# ### 6.2 Introduction to algorithms

The process of computational problem-solving should be familiar to anybody with even a basic mathematical education. Given a real-world problem, it's the job of mathematicians (the 'computers' of these problems) to do two things: model the problem in the language of mathematics (maths), and then apply mathematical tools to that model to produce a solution. To highlight how fundamental this process is, consider the following trivial maths questions:

Sarah has nine apples. John takes two of Sarah's apples from her. How many apples does Sarah have left?