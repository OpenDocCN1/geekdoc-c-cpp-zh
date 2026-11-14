The security considerations should address:

+   - Potential vulnerabilities.
+   - Potential pre-, during, and post-attack defense strategies.

With respect to reliability, one can specify:

+   - The system uptime goals.
+   - Potential risks, failures, and failure modes.
+   - Failure management strategy.

# Example 9.1 IDENTIFYING THE REQUIREMENTS
Designing a Counter (cont.)

Starting from the trip report from High Flying Avionics, Inc., which discussed its needs for a new counter, let's put the requirements specification together.

As a first step in the thought process, one extracts and summarizes the essential information from the trip report. By doing so, one can begin to focus on what should be included in the requirements specification. From the discussions with the customer, a high-level sketch of the system and the environment captures the essential parts of the problem. The next step is to begin to formalize the model of the system and the environment, as illustrated in Figure 9.24. Let's put the Requirements Specification together.

![](bbox=[0.275, 0.42, 0.75, 0.62])

# Figure 9.24 The System and Its Environment – Step 2

In its initial configuration, the environment contains:

+   - A set of navigation radios that are to be tested.
+   - The user who is doing the testing.
+   - The factory.

Signals flow from the navigation radio to the counter, but not the reverse. The factory has inputs to the counter as well; these include the power system and the ambient environment in the factory. The user interaction is bidirectional. The user must select and configure the measurement to be made and then view the results once the measurement is complete. For the computer, the signal interchange with the counter similarly occurs in both directions.