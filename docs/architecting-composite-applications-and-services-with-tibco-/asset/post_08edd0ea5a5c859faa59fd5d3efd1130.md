
## Benchmarking

### Objectives

A benchmark is a standard against which things can be compared. The term is also used to refer to a standardized test or experiment with results, that when the test is applied to different systems, can be used to compare those systems.

In the development environment, these two meanings are practically inseparable. The benchmark results (i.e., the standard) can only be understood by understanding both the test that produced the results and the configuration of the system under test. Two sets of results from two different systems cannot be fairly compared unless the same test was used and the configurations of both systems are clearly understood. In fact, if there isn’t enough information for you to reproduce the test results, there isn’t enough information for you to understand and apply those results to your situation!

This chapter discusses the conduct of benchmark tests and documentation that is required for the test results to be meaningful to other people. After reading this chapter, you will be able to

- Describe how a benchmark test should be conducted.
- Describe how benchmark tests results should be documented.
- Describe how to benchmark complex components.
- Identify the resource with a limitation that determines a component’s capacity.

### Misleading Results

### The Bathtub Test

Imagine wanting to benchmark the rate at which you can consume water. In designing the test, you want to ensure that your measurement is not adversely impacted by a limitation in the available supply of water. Consequently, you design the test to drink from a high-pressure fire hose.

There’s no question here that the hose can supply water at a faster rate than you can drink, but is this a fair test of capacity? When you run the test, you find yourself gasping for air and trying to keep from drowning, activities that certainly detract from your optimal consumption of water. The test is, somehow, flawed, at least with respect to measuring your drinking capacity.

Although this example is a bit absurd, it serves to illustrate a common flaw in what are purported to be capacity measurement tests. In message-based systems, these often take the form of loading up a message queue with millions of messages, turning on the message consumer, and looking at the rate at which the consumer actually processes the messages. This is often referred to as the bathtub test and, in reality, it is not a capacity measurement at all but rather an overload test. Let’s see why.

Figure 14-1 shows a typical performance curve for a component. The horizontal axis shows the steady-state rate at which inputs are presented to the component, and the vertical axis shows the steady-state rate at which the component completes the work, here characterized as

![](img/b8d8132a583ad73d511c4c1bb92e2df7_350_0.png)

Figure 14-1: Typical Performance Curve

the production of an output. Over some range of input rates, the output rate exactly tracks the input rate: The component is performing work at the same rate at which it is being presented with work.

As the input rate increases you eventually reach a point beyond which the component can no longer keep up with the increasing demand. This is the point that defines the operating capacity of the component.

Beyond the operating capacity, you are in the overload region and the behavior of the component is different. Inputs are arriving faster than they are being processed, and either they are being lost altogether or they are piling up in a buffer. If they are piling up in a buffer, that buffer has a finite capacity, and when you reach that capacity something bad is going to happen. Therefore, extended operation in this region is inherently unstable.

But there are consequences for operating in the overload region even before it becomes unstable. Resources that would otherwise be applied to doing useful work with the component are now being dedicated to managing the buffer. Initially, this may just manifest itself as a falling-off of output rate, but as the input rate increases further, the output rate levels off and then begins to decline. It typically declines to some level substantially below the nominal operating capacity of the component.

The bathtub test (or fire hose test) immediately pushes the component well into the overload region. Even though it may be useful in determining whether a component is well behaved (at least for some period of time) when overloaded, it does not give you any true indication of the component’s operating capacity.

### Disabling Features

Another common source of misleading results is running the benchmark test on a component that is not configured as it would be in production. Some common examples are

- Using asynchronous disk writes for benchmarking when synchronous interaction will be used in production
- Running without security policies in place when security policies will be used in production
- Running without transaction management when transactions will be used in production
- Running without logging when logging will be used in production

### Test Harness Design

Inappropriate design of test harnesses can also lead to misleading results. For example, it is common to use a Java sleep() operation to introduce a delay in a loop that sends inputs to the component under test. However, this operation generally takes a millisecond or longer to execute, even if the specified time delay is zero. Thus the maximum rate at which this loop can generate inputs is less than 1,000 per second.

Gathering the data can also have an impact on the measured test results. The techniques used for data capture and recording require careful consideration. If these activities are being performed on the machine upon which the component under test is running, they will consume machine resources and thus reduce the apparent capacity of the component.

### Determining Operating Capacity

In order to effectively determine the operating capacity of a component, you need a test setup similar to that shown in Figure 14-2. In addition to the system under test, this test setup has three essential ingredients:

- 1. A mechanism for supplying inputs at a controlled rate
- 2. A mechanism for measuring the actual input rate
- 3. A mechanism for measuring the work completion rate (typically a result or output)

![](img/b8d8132a583ad73d511c4c1bb92e2df7_352_0.png)

Figure 14-2: Test Setup for Determining Operating Capacity

![](img/b8d8132a583ad73d511c4c1bb92e2df7_354_0.png)

(a) Request-Reply Test Setup

![](img/b8d8132a583ad73d511c4c1bb92e2df7_354_1.png)

(b) Straight-through Processing Test Setup

### Figure 14-3: Test Design Architecture Pattern Examples

under test and not the test harness. Test harnesses should be run in their own dedicated machines. To fully load the component under test or to handle the volume of output, multiple instances of the test harnesses may be required, possibly running on multiple machines.

Communications infrastructure needs to be considered as well, particularly if the component you are testing is a messaging server. The Enterprise Message Service, when run on an appropriate platform, can saturate 100 Mbit and 1 Gbit networks—and possibly even 10 Gbit networks.

The details of the test environment must also be documented. Here you must use some discretion as to the necessary level of detail, but the governing criteria should be whether the detailed item might impact the test results. Table 14-1 shows a typical set of details for the machine on which the component under test is being run. Table 14-2 shows the setup for the machine running the test harness, and Table 14-3 shows the network details.

### Test Harness Process Mapping

For most tests, the process design is trivial: Send a request, get a reply. There is little benefit in documenting the process by itself, and so attention immediately turns to the mapping of the process onto the architecture pattern. Figure 14-4 shows such a mapping for a simple request-reply test scenario.
