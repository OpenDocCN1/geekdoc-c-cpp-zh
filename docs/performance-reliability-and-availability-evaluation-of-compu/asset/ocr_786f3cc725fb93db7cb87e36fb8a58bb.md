# Fault Injection and Failure Monitoring

![](bbox=[0.198, 0.101, 0.813, 0.563])

**Figure 26.5** An Architecture of Generic Fault Injection Tool.

The Statistics Library provides a set of statistical methods for parameter estimation. The Probability Distributions Library supports random variable generation, probability calculation, and moments estimation. The Models’ Library stores a set of models that can be reused when building a new fault injection plan. The Fault Mechanisms’ Library provides a set of methods for injecting or emulating a fault in a system or even for simulating faults if the system under test is still a summative model. The User Interface Library provides a function for supporting the interaction between the Fault Injector and the operator. Finally, the Context-Specific Library provides a set of functions customized for each particular system test.

The system under test may be a system that does not share the same hardware infrastructure as Figure 26.5 suggests or may be a software system that shares the same hardware infrastructure of the computer that injects faults in SUT. For example, Figure 26.6 shows a software system under test (SUT) that shares the same hardware