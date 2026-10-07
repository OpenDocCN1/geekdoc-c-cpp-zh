
# Workload Characterization

User's Desktop

![](img/2d1450514bb14a0cdf0eb5048614afab_493_0.png)

Figure 24.3 WGCap-Capacity Advisor Interaction.

## 24.3 WORKLOAD MODELING

A computer system workload model represents a workload of the computer system. Such a model may be adopted to analyze scenarios of interest that the performance analyst is required to evaluate via closed-form formulas, numerical analysis, or simulation. Such a model may also be adapted to generate actual system workloads or generate synthetic workloads. However, workload characterization is not always straightforward due to the required level of detail in which the workload should be represented and which aspects of the workload are significant.

Workloads can be described by their:

- (a) intended work or can be described by the
- (b) impact on the computer system resources

Figure 24.4 shows these perspectives highlighted above. In the latter case, the impact of the workload on the system is represented by statistical summaries and probabilistic distributions of the system’s resource utilization, throughput, and time required for resources to process the computer system demand (see Section 8.3).

![](img/2d1450514bb14a0cdf0eb5048614afab_494_0.png)

Figure 24.4 Workload Point of Views: Intended Work or Impact on Resources.

The workload may also be represented by the intended work, that is, by what, when, and how often the system should perform the related activities. However, let us first consider the case in which the workload is described by its impact on the computer system (descriptive models).

### 24.3.1 MODELING WORKLOAD IMPACT

Statistical and probabilistic modeling of the workload impact of system infrastructure involves sampling the usage, throughput, discard rates, delays related to the selected resources of interest, obtained statistical summaries, and probability distributions that represent the representative samples. We illustrate this general approach by using a set of examples.

Example 24.3.1. Assume a computer system with a Linux operating system executes the following script (already shown when studying Linpack benchmark):

# scriptlinpack

```bash
printf "Linpack Results \n" >> Linpack_result.txt;
for i in {1..100}
do
  Linpack >> Linpack_result.txt;
done,
```

where Linpack is the executable file of the Linpack benchmark (see Section 24.2.1 and Appendix C). Each execution of the file Linpack provides the respective execution time and the float-point instructions per second of each execution, among other data.

The scriptlinpack executes the Linpack benchmark one hundred times and writes the benchmark results in the file Linpack_result.txt. After starting the script's execution, the following command was executed in another command-line interface (shell):

```bash
> pidstat -u -C "Linpack" 1 >> Linpack_uti_result.txt
```

The execution of the command-line above looks up any process filename linpack and measures its processor utilization. The utilization measures with delay between measures equal to one. The utilization measures are stored in the file Linpack_uti_result.txt. When the script ends execution, the monitoring started may be finished by executing the command Ctrl+C. As the monitoring started after the scriptlinpack runs, being eighty-one (C0=81)-The number of completed tasks according to the notation in Chapter 8 out of one hundred Linpack executions were measured. The content of the file Linpack_uti_result.txt is shown in Table 24.9.

#### Table 24.9 Content of the File Linpack uti_result.txt

| Time | PM | PID | %usr | %system | %guest | %CPU | CPU | Command |
|---|---|---|---|---|---|---|---|---|
| 3:12:59 | PM | 25432 | 53.47 | 0 | 0 | 53.47 | 0 | Linpack |
| 3:13:00 | PM | 25433 | 48.35 | 0 | 0 | 48.35 | 0 | Linpack |
| 3:13:01 | PM | 25434 | 47 | 0 | 0 | 47.00 | 0 | Linpack |
| 3:13:02 | PM | 25435 | 43 | 0 | 0 | 43.00 | 0 | Linpack |
| 3:13:03 | PM | 25436 | 47 | 0 | 0 | 47.00 | 0 | Linpack |
| 3:13:04 | PM | 25437 | 49.5 | 0 | 0 | 49.50 | 0 | Linpack |
| 3:13:05 | PM | 25438 | 53.06 | 0 | 0 | 53.06 | 0 | Linpack |
| 3:13:06 | PM | 25439 | 55 | 1 | 0 | 56.00 | 0 | Linpack |
| 3:13:07 | PM | 25440 | 56 | 1 | 0 | 57.00 | 0 | Linpack |
| 3:13:08 | PM | 25441 | 53 | 0 | 0 | 53.00 | 0 | Linpack |
| 3:13:09 | PM | 25442 | 51 | 0 | 0 | 51.00 | 0 | Linpack |
| 3:13:10 | PM | 25443 | 36.96 | 0 | 0 | 36.96 | 0 | Linpack |
| (Continued) |

#### Table 24.9 Content of the File Linpack utl result

| Time | PM | PID | %usr | %system | %guest | %CPU | CPU | Command |
|---|---|---|---|---|---|---|---|---|
| 3:13:11 | PM | 25444 | 38 | 0 | 0 | 38.00 | 0 | Linpack |
| 3:13:12 | PM | 25445 | 31 | 0 | 0 | 31.00 | 0 | Linpack |
| 3:13:13 | PM | 25446 | 21 | 0 | 0 | 21.00 | 0 | Linpack |
| 3:13:14 | PM | 25447 | 24 | 0 | 0 | 24.00 | 0 | Linpack |
| 3:13:15 | PM | 25448 | 27 | 0 | 0 | 27.00 | 0 | Linpack |
| 3:13:16 | PM | 25449 | 29.7 | 0 | 0 | 29.70 | 0 | Linpack |
| 3:13:17 | PM | 25450 | 34.3 | 0 | 0 | 34.34 | 0 | Linpack |
| 3:13:18 | PM | 25451 | 28.7 | 0 | 0 | 28.71 | 0 | Linpack |
| 3:13:19 | PM | 25452 | 31 | 2 | 0 | 33.00 | 0 | Linpack |
| 3:13:20 | PM | 25453 | 33.6 | 0 | 0 | 33.68 | 0 | Linpack |
| 3:13:21 | PM | 25454 | 34 | 1 | 0 | 35.00 | 0 | Linpack |
| 3:13:22 | PM | 25455 | 23.6 | 0 | 0 | 23.76 | 0 | Linpack |
| 3:13:23 | PM | 25456 | 11.1 | 0 | 0 | 11.11 | 0 | Linpack |
| 3:13:37 | PM | 25467 | 89.1 | 0.99 | 0 | 90.10 | 0 | Linpack |
| 3:13:38 | PM | 25470 | 93 | 0 | 0 | 93.00 | 0 | Linpack |
| 3:13:39 | PM | 25471 | 84 | 0 | 0 | 84.00 | 0 | Linpack |
| 3:13:40 | PM | 25472 | 72.3 | 0 | 0 | 72.73 | 0 | Linpack |
| 3:13:41 | PM | 25473 | 68.3 | 0 | 0 | 68.37 | 0 | Linpack |
| 3:13:42 | PM | 25474 | 68.3 | 0 | 0 | 68.37 | 0 | Linpack |
| 3:13:43 | PM | 25475 | 65 | 0 | 0 | 65.00 | 0 | Linpack |
| 3:13:44 | PM | 25476 | 71 | 0 | 0 | 71.00 | 0 | Linpack |
| 3:13:45 | PM | 25477 | 69 | 0 | 0 | 69.00 | 0 | Linpack |
| 3:13:46 | PM | 25478 | 74 | 0 | 0 | 74.00 | 0 | Linpack |
| 3:13:47 | PM | 25479 | 78 | 0 | 0 | 78.00 | 0 | Linpack |
| 3:13:48 | PM | 25480 | 80 | 1 | 0 | 81.00 | 0 | Linpack |
| 3:13:49 | PM | 25481 | 86 | 0 | 0 | 86.00 | 0 | Linpack |
| 3:13:50 | PM | 25482 | 80.8 | 0 | 0 | 80.81 | 0 | Linpack |
| 3:13:51 | PM | 25483 | 85 | 0 | 0 | 85.00 | 0 | Linpack |
| 3:13:52 | PM | 25484 | 89.9 | 0 | 0 | 89.90 | 0 | Linpack |
| 3:13:57 | PM | 25490 | 14 | 0 | 0 | 14.00 | 0 | Linpack |
| 3:13:58 | PM | 25491 | 16.33 | 0 | 0 | 16.63 | 0 | Linpack |
| 3:13:59 | PM | 25492 | 20 | 0 | 0 | 20.00 | 0 | Linpack |
| 3:14:00 | PM | 25493 | 15 | 0 | 0 | 15.00 | 0 | Linpack |
| 3:14:01 | PM | 25494 | 19.8 | 0 | 0 | 19.80 | 0 | Linpack |
| 3:14:02 | PM | 25495 | 26.6 | 0 | 0 | 26.26 | 0 | Linpack |
| 3:14:04 | PM | 25506 | 51.06 | 0 | 0 | 51.06 | 0 | Linpack |
| 3:14:05 | PM | 25500 | 82.14 | 7.14 | 0 | 89.29 | 0 | Linpack |
| 3:14:15 | PM | 25501 | 75 | 0 | 0 | 75.00 | 0 | Linpack |
| 3:14:19 | PM | 25508 | 10 | 0 | 0 | 10.00 | 0 | Linpack |
| 3:14:20 | PM | 25509 | 14 | 0 | 0 | 14.00 | 0 | Linpack |
| 3:14:21 | PM | 25510 | 10.89 | 0 | 0 | 10.89 | 0 | Linpack |
| 3:14:22 | PM | 25511 | 16 | 0 | 0 | 16.00 | 0 | Linpack |

(Continued) |

![](/2d1450514bb14a0cdf0eb5048614afab_496_0.png)

#### Table 24.9 Content of the File Linpack ut result

| Time | PM | PID | %usr | %system | %guest | %CPU | CPU | Command |
|---|---|---|---|---|---|---|---|---|
| 3:14:23 | PM | 25512 | 19.19 | 0 | 0 | 19.19 | 0 | Linpack |
| 3:14:24 | PM | 25513 | 22.77 | 0 | 0 | 22.77 | 0 | Linpack |
| 3:14:25 | PM | 25514 | 27 | 0 | 0 | 27.00 | 0 | Linpack |
| 3:14:26 | PM | 25515 | 30 | 0 | 0 | 30.00 | 0 | Linpack |
| 3:14:27 | PM | 25516 | 20 | 0 | 0 | 20.00 | 0 | Linpack |
| 3:14:29 | PM | 25517 | 95 | 0 | 0 | 95.05 | 0 | Linpack |
| 3:14:30 | PM | 25518 | 91 | 0 | 0 | 91.00 | 0 | Linpack |
| 3:14:31 | PM | 25519 | 91 | 0 | 0 | 91.00 | 0 | Linpack |
| 3:14:32 | PM | 25520 | 82 | 0 | 0 | 82.00 | 0 | Linpack |
| 3:14:33 | PM | 25521 | 83 | 0 | 0 | 81.30 | 0 | Linpack |
| 3:14:34 | PM | 25522 | 77 | 0 | 0 | 77.00 | 0 | Linpack |
| 3:14:35 | PM | 25523 | 78 | 0 | 0 | 78.00 | 0 | Linpack |
| 3:14:36 | PM | 25524 | 84 | 0 | 0 | 84.00 | 0 | Linpack |
| 3:14:37 | PM | 25525 | 88.1 | 0 | 0 | 88.12 | 0 | Linpack |
| 3:14:38 | PM | 25526 | 84.27 | 0 | 0 | 84.27 | 0 | Linpack |
| 3:14:39 | PM | 25527 | 69 | 0 | 0 | 69.31 | 0 | Linpack |
| 3:14:40 | PM | 25528 | 61 | 0 | 0 | 62.00 | 0 | Linpack |
| 3:14:41 | PM | 25529 | 58 | 0 | 0 | 58.00 | 0 | Linpack |
| 3:14:42 | PM | 25530 | 52.53 | 0 | 0 | 52.53 | 0 | Linpack |
| 3:14:43 | PM | 25531 | 44.55 | 0 | 0 | 44.55 | 0 | Linpack |
| 3:14:44 | PM | 25532 | 34 | 1 | 0 | 35.00 | 0 | Linpack |
| 3:14:45 | PM | 25533 | 30 | 0 | 0 | 30.00 | 0 | Linpack |
| 3:14:46 | PM | 25534 | 24 | 0 | 0 | 24.00 | 0 | Linpack |
| 3:14:47 | PM | 25535 | 22.77 | 0 | 0 | 22.77 | 0 | Linpack |
| 3:14:48 | PM | 25536 | 14 | 0 | 0 | 14.00 | 0 | Linpack |
| 3:14:49 | PM | 25537 | 16.16 | 0 | 0 | 16.16 | 0 | Linpack |
| 3:14:50 | PM | 25538 | 21.21 | 0 | 0 | 21.21 | 0 | Linpack |
