# # Hardware Test and Debug

# ## THINGS TO LOOK FOR ...

+   - The vocabulary of testing.
+   - The reasons for debugging, troubleshooting, and testing.
+   - The need for planning, specifications, test procedures, and test cases.
+   - Steps and heuristics for the debugging process.
+   - Identification and isolation of common faults in combinational and sequential circuitry.
+   - Tests for the designer and for the customer.

# ## 10.1 INTRODUCTION

Formulating a testing, debugging, or troubleshooting strategy should occur early in the design and development process. Ideally, it should be concurrent with the hardware and software development.

Most often, when we come up with an idea for any new design, we begin with a plan. We think about what the system will do; we think about its features, its capabilities, and its functionality. Debugging, troubleshooting, and testing are no different. We must have a plan. Without a plan, we can’t be sure what we are looking for, or what it might look like if we find it, or when we are finished.

We will begin the study of test by introducing some of the relevant vocabulary. Understanding the terminology facilitates understanding the requirements of a test or test strategy, as well as the capabilities and limitations of the equipment utilized to execute the strategy. Earlier discussions of the effects of microprocessor word size on real numbers and subsequent computations now provide a basis for understanding, formulating, and interpreting measurements during the test process. We will then present a high-level model for a testing strategy; examine and motivate the need for planning, specifications, test procedures, and test cases; and examine several views, ranging from black to white box models, for approaching test. Finally, we will move into testing during the different stages of the product life cycle.

# ## 10.2 SOME VOCABULARY

As a prelude to the study of debugging and testing, it is important to understand some of the vocabulary of the area. Making measurements or generating signals is rather