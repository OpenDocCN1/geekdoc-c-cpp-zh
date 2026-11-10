| Program | Application | Description |
|---|---|---|
| RVASSO | SD | Creates billing documents |
| RAALT011 | AM | Direct data import for asset accounting |
| RKEVEXTG | CO-PA | Transfers external data to CO-PA |

**Table 19.1** Direct Input Programs (Cont.)

A direct input program is faster than a batch input program because it doesn't depend on transaction screens to validate the data. Direct input programs are executed in the background and support error reporting. In case of any errors, the data transfer can be resumed after correcting the errors. A background job can be scheduled to run the programs at regular intervals.

Direct input programs are run in the background and managed using Transaction BMVO (see Figure 19.1). Running direct input programs in the background is the preferred method for production runs, but you can also execute these programs in the foreground for testing the data transfers.

The program documentation for each of the direct input programs provides more information on their usage.

![](bbox=[0.148, 0.522, 0.666, 0.743])

**Figure 19.1** Direct Input Management

# 19.1.2 Batch Input

Unlike direct input programs, batch input programs rely on the corresponding transactions to validate the data. Batch input programs allow you to capture the steps involved in processing the data and automate this process.