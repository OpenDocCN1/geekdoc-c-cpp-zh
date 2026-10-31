
## Individual Activity Benchmarks

Once the baseline overhead has been established, you can begin to benchmark individual activities. For each activity of interest, add the activity to one of the test scenarios for which you have a baseline overhead benchmark. Repeat the baseline test with the activity added, with an initial focus on minimizing the amount of work done in the activity. The difference between the baseline results and this set of results gives you the overhead of executing the activity you are testing.

Once the overhead for the activity has been established, you can identify the parameters that might impact its execution. In addition to those mentioned before (test harness and component parameters), you probably want to look at the possible configurations of the activity itself. For example, if you are looking at the data transformation activity in ActiveMatrix BusinessWorks, you might want to consider varying the size of the data structure, the complexity of the data structure, and the complexity of the transformation. To keep this from becoming an open-ended experiment, you need to have some idea of how this activity will be used in your solution and make sure that your experiments reflect the nature of that use.

As with the overhead measurements, once you have identified the relevant parameters, you want to repeat the baseline test for each new parameter setting. This set of results will help you understand the resource requirements for the activity.

Be cautious in your evaluation of activities that rely on other components. Interactions with the file system, databases, and messaging services will depend as much on the performance of those components as they will on the component you are trying to benchmark. Make sure you understand and account for those external components.

## Benchmark Common Scenarios in which Activities Interact

Over time you will come to recognize certain component usage patterns that arise repeatedly in your design. For example, you might have many cases in which a front-end system makes a SOAP over JMS call to a service implemented in ActiveMatrix BusinessWorks, and this service does a database lookup and returns the results. When you look at the BusinessWorks design, you have a Service that invokes a process containing a JDBC activity with data transformations before and after the JDBC activity. Since this is a common pattern appearing in many solutions, it makes sense to invest in benchmarking its performance. This will provide the data you need to do capacity planning when this pattern is employed.

## Interpreting Benchmark Results

So you are running a benchmark test and, looking at the input and output rates, you identify what appears to be the operating capacity. You’d like to know, first of all, that the component is truly running at its maximum capacity and what resource limitation ultimately determined that capacity. This section provides you with some information you can use to help answer these questions.

When you graph resource utilization data against input rate, the resulting curves give you the information you need to determine which resource is the limiting factor in performance. The following sections show how you can use these curves to identify the resource limitations listed here:

- CPU
- Network bandwidth
- Disk performance
- Memory
- Test harness limitations

### Identifying the Capacity Limit

The first step in identifying the resource limitation is to establish the nominal operating capacity as determined by your present benchmark test results. This is done by graphing the input versus output rate, as was done in Figure 14-7, and identifying the point at which the input/output curve begins to deviate from a 45-degree slope. Graphing latency as well (Figure 14-8) can help identify the operating capacity: You’ll usually see a sharp change in the slope of the latency curve when you reach the operating capacity.

There is an additional feature of this graph that is worth noting: As the message rate is increased beyond the operating capacity, a second break in both the output and latency curves occurs. The output rate drops near zero, and the latency jumps way up. At this point, the data structures had to be increased to 100 KB. Showing the actual network interface card (NIC) bandwidth on the graph makes it even clearer that the bandwidth limit has been reached. Note that in this case the operating capacity is now lower than before.

There is an important lesson in this example regarding test harness and component parameters: The settings of these parameters can alter the apparent capacity of the component under test, often erroneously. In this case, the test never reached the operating capacity of the component under test. Instead, it ran into what might be best described as a test harness limitation: It ran out of network bandwidth.

On numerous occasions TIBCO customers have reported supposedly poor benchmark results with Enterprise Message Service only to discover upon investigation that they had run into a network bandwidth limitation such as a 10 Mbit or 100 Mbit NIC card or switch. This is why it is so important to graph resource utilization in these benchmark tests so that you really understand the nature of the limit you have encountered.

### Identifying Disk Performance Limits

Identifying disk performance limits is complex, for a variety of reasons. Nevertheless, it is an important consideration. As with network bandwidth, it is not practical in most environments to measure disk access. You have to work with computations—estimates.

Disk performance shows up in a variety of guises. The obvious cases are file operations being performed by the component. A bit less obvious are the database accesses. If you have appropriate benchmarks for the database that reflect your component’s usage patterns, you can use those. However, if you are designing your own database you may have to do your own benchmark or, failing that, your own estimates.

There are two different types of measurements that are relevant to disk access. One is the rate at which requests for disk access occur, which is commonly measured in terms of I/O operations per second (IOPS). The other is the rate at which data is being transferred to and from the disk, commonly referred to as the disk data transfer rate and is measured in bytes/second.

It also makes a difference whether the component is reading or writing to the disk: Read requests can be answered from a cached buffer, so you need some estimate as to the likelihood that the result you are looking for is already in the cache. Write performance depends upon the writing strategy: synchronous or asynchronous. Synchronous

Seek time reflects the time it takes for the disk head to move to the proper track.

avgAccessRate_accesses/sec = 1 / (avgSeekTime_sec + avgRotationalLatency_sec + dataTransferTime_sec)

The seek time for the disk being used as an example is 2 milliseconds. The sum of the seek time and average rotational latency is 5 milliseconds. The data transfer time is so small in relation to this value that it can be ignored. This yields an average access rate of 200 accesses per second (IOPS) for this single disk.

The specifications for solid-state drives generally give the access time or rate and the read and write rates. Typical numbers at the time of this writing are random reads at 40,000 IOPS, random writes at 50,000 IOPS, sequential read data rates at 415 MB/second and write data rates at 260 MB/second.

Calculating access rates for RAID arrays is significantly complicated, as it depends upon the type of disk, the number of spindles in the array, the RAID configuration, the mixture of read and write operations, and the size of the dataset being transferred. There are a number of online calculators that you can use to determine the actual rates, such as Marek Wolynko's IOPS calculator at http://www.wmarow.com/. For a comprehensive discussion of RAID array performance, see Chapter 3 of Somasundaram and Shrivastava's Information Storage and Management: Storing, Managing, and Protecting Digital Information.¹

Calculations for storage subsystems, particularly those with battery-backed memory, are so dependent upon the design of the storage subsystem and the mechanisms used to access them that you will have to search online or consult the vendor to determine the characteristics of the system you are using.

Contention for the disk is another issue you need to take into consideration. Disks tend to be shared resources, and it is often difficult to determine the actual level of disk utilization. For this reason, your computations regarding disk performance should be taken as upper

1. G. Somasundaram and Alok Shrivastava, Information Storage and Management: Storing, Managing, and Protecting Digital Information, Indianapolis: John Wiley & Sons (2009).

## 视觉SLAM (VSLAM)

视觉SLAM（Simultaneous Localization and Mapping，同时定位与地图构建）是指利用摄像头采集的图像信息，实时估计自身位置并构建环境地图的技术。它广泛应用于自动驾驶、移动机器人、增强现实（AR）和无人机导航等领域。

### 核心流程

- 传感器数据采集
- 前端视觉里程计（VO）
- 后端优化（BA）
- 回环检测
- 建图

### 相机模型

常用的相机模型包括针孔模型和鱼眼模型。针孔模型适用于常规视角，鱼眼模型适用于广角场景。

![](img/b8d8132a583ad73d511c4c1bb92e2df7_366_0.png)

### 特征点法

特征点法通过提取图像中的关键点（如ORB、SIFT）并进行描述子匹配来估计相机运动。

### 关键帧与BA优化

| 方法   | 精度   | 实时性 | 鲁棒性 |
|--------|--------|--------|--------|
| 特征点法 | 高 | 中 | 高 |
| 直接法 | 中 | 高 | 中 |

> VSLAM 是机器人感知与导航的核心技术之一。

```python
import numpy as np
def estimate_pose(points_2d, points_3d):
    # 调用PnP求解
    return np.eye(4)
```
