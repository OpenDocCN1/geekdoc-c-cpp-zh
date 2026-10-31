
![](img/b8d8132a583ad73d511c4c1bb92e2df7_357_0.png)

Figure 14-5: Two-threaded Test Harness Mapping

approach might be to use a multi-threaded design for the test harness (Figure 14-5). Alternatively, you may want to deploy multiple instances of the test harness, potentially on multiple machines. However, regardless of the approach taken, it is incumbent on the test designer to document the design and configuration of the test harness so that the reader of the test results is in a position to evaluate the harness design and its likely impact on the test results.

## Experimental Parameters

Often there are parameters that can be varied in the experiment. The variables that are important depend on the nature of the components and the nature of the tests being performed. In conducting your benchmarks, you will have to determine which parameters are important for your benchmarks. Some common examples include

- Test harness parameters
  - Degree of parallelism required to fully load the component (e.g., number of test harnesses or number of threads in each test harness)
  - Size of data set
- Component under test parameters
  - Number of threads in the component
  - The number of concurrent sessions allowed (e.g., the value of the ActiveMatrix BusinessWorks MaxJobs parameter)
  - Constraints on the number of activities that can occur in parallel (e.g., the sequencing key in ActiveMatrix BusinessWorks)
  - Sizes of buffers (e.g., prefetch settings on Enterprise Message Service clients)
  - The number of connections allowed

Some of these parameters will remain the same for all test runs, while others you will intentionally vary to determine their impact on the component’s performance. For each test run, the values of all parameters must be documented.

## Test Results

The final aspect of the test that must be documented is the data that was collected (Figure 14-6). This data includes the test parameter settings and all of the measurements that were made. Once again, decisions have to be made about what to measure, and the criteria should be things that might impact the test results. Typical measurements include (in addition to input and output rates) calculated data rates, latency, CPU utilization, memory utilization, disk access rate, disk bandwidth utilization, and network bandwidth utilization. Note that the disk and network numbers are generally calculations based on other measurements and settings (input rate, message size) and an understanding of component behavior.

To make the data more useful, it is a good idea to provide the data in graphical form as well. Figure 14-7 shows the basic input versus output rate graph. Note the falloff of the output rate as the input rate rises. This is a clear indication that the operating capacity has been identified, assuming that the appropriate tuning adjustments have already been done.

**Experimental Parameters**

|  |  |
|---|---|
| Message Size (KB) | 5 |
| Worker Threads | 10 |

**Test Data**

| Input Message Rate (messages/sec) | Input Data Rate (KB/sec) | Output Message Rate (messages/sec) | Output Data Rate (KB/sec) | Latency (ms) | CPU Utilization (% of available CPU) | RAM Utilization (MB) | Disk Access Rate (accesses/sec) | Disk Bandwidth Utilization (MB/sec) | Network Bandwidth Utilization (KB/sec) |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 5 | 1 | 5 | 2 | 0% | 150 | 3 | 0 | 10 |
| 2 | 10 | 2 | 10 | 2 | 0% | 150 | 6 | 0 | 20 |
| 5 | 25 | 5 | 25 | 3 | 0% | 150 | 15 | 0 | 50 |
| 10 | 50 | 10 | 50 | 3 | 1% | 151 | 30 | 0 | 100 |
| 20 | 100 | 20 | 100 | 4 | 1% | 151 | 60 | 0 | 200 |
| 50 | 250 | 50 | 250 | 4 | 3% | 153 | 150 | 1 | 500 |
| 100 | 500 | 100 | 500 | 5 | 5% | 155 | 300 | 2 | 1,000 |
| 200 | 1,000 | 200 | 1,000 | 5 | 10% | 160 | 600 | 3 | 2,000 |
| 500 | 2,500 | 500 | 2,500 | 6 | 25% | 175 | 1,500 | 8 | 5,000 |
| 1,000 | 5,000 | 1,000 | 5,000 | 6 | 50% | 200 | 3,000 | 15 | 10,000 |
| 2,000 | 10,000 | 1,250 | 6,250 | 10 | 100% | 250 | 3,750 | 19 | 16,250 |
| 5,000 | 25,000 | 800 | 4,000 | 38 | 100% | 400 | 2,400 | 12 | 29,000 |
| 10,000 | 50,000 | 500 | 2,500 | 120 | 100% | 650 | 1,500 | 8 | 52,500 |
| 20,000 | 100,000 | 350 | 1,750 | 343 | 100% | 1,150 | 1,050 | 5 | 101,750 |
| 25,000 | 125,000 | 1 | 5 | 150,000 | 100% | 1,400 | 3 | 0 | 125,005 |

Figure 14-6: Test Data Example

![](img/b8d8132a583ad73d511c4c1bb92e2df7_360_0.png)

Figure 14-7: Graph of Input versus Output Rates

## Benchmarking Complex Components

Benchmarking complex components is, well, complex! Such components typically perform multiple activities, and these activities can be of different types. Complicating things further, different types of activities may consume different levels of resources. Components that manage processes fall into this category, with ActiveMatrix BusinessWorks and TIBCO ActiveMatrix® BPM being common examples.

What makes the benchmarking of these components complex is that there are virtually an infinite number of ways in which the activities can be combined into processes that are then executed by the components. The likelihood that your process will be similar enough to a given benchmark process for those benchmark results to be useful is very small. So how do you go about establishing useful benchmarks for components like these?

The answer is to obtain data about individual aspects of component behavior that you can then combine analytically to get some reasonable estimate of your design’s performance. So what data do you need? In general, you need three kinds:

1. Overhead benchmarks
2. Individual activity benchmarks
3. Common scenario benchmarks

### Overhead Benchmarks

Simply interacting with a component has some overhead associated with it. The idea of overhead benchmarks is simply to understand what this overhead is. To make such measurements, you want to identify the simplest (lightest weight) activities that the component is capable of doing. For ActiveMatrix BusinessWorks, this might simply be returning an inbound message. For ActiveMatrix® BPM, this might be starting a trivial business process (one with one activity and no data) or performing an activity that does no work.

The measurements you get from overhead tests will give you an upper bound on what is possible. If you find the maximum rate at which ActiveMatrix BusinessWorks can start a trivial process that just returns a result, adding work to that process can only lower the rate. However, understanding that maximum rate in itself gives you important information. If your solution requires a particular piece of work to be done at a particular rate and that rate exceeds (or even comes close to) the maximum for a BusinessWorks instance, you know immediately that it will take multiple instances of BusinessWorks to do the job.

When setting up overhead benchmarks, the first thing you need to do is identify the basic scenarios to be tested. For ActiveMatrix BusinessWorks, this might be the running of a trivial process. For ActiveMatrix BPM, this might be the starting of a trivial process and the execution of a trivial activity. To aid you in identifying the scenarios, think about the way in which the component will interact with the other solution components, and then ask yourself what patterns are involved and what constitutes a “minimal” version of each scenario. When identifying the scenarios, take the interaction mechanism into account: A SOAP over HTTP interaction will have different overhead than a SOAP over JMS interaction.

Once you have identified the relevant scenarios, you then run a baseline performance test for each scenario as described in the previous section. Keep data structures minimal in size.

After the baseline has been established, identify the parameters that might affect the result. These may be test harness parameters (e.g., message size) or component parameters (e.g., the number of worker threads in ActiveMatrix BusinessWorks). For each of the parameters, define a range of values to be tested. Then, for each parameter value, repeat the entire baseline performance test.
