

导致驱动程序调用序列化。因此，查询事件队列的修订代码如下：

```
printf("\nWaiting");

u32 results_to_process = num_devices;
u32 sleep_count = 0;
// While there are results still to process
while(results_to_process != 0)
{
    // Process the data as it comes back from the GPUs
    // Overlaps CPU execution with GPU execution
    for (int device_num=0;
        device_num < num_devices;
        device_num++)
    {
        // If results are pending from this device
        if (processed_result[device_num] == false)
        {
            // Try to process the data from the device
            processed_result[device_num] =
                process_result(device_num);
        }

        // If we were able to process the data
        if (processed_result[device_num] == true)
        {
            // Then decrease the number of pending
            // results
            results_to_process--;
        }

        // print the time host waited
        printf("%sHost wait time : %u ms\n",
            device_prefix[device_num],
            sleep_count * 100);

        // If there are still more to process
        // print start of progress indicator
        if (results_to_process != 0)
            printf("\nWaiting");
    }
    fflush(stdout);
}
else
{
    printf(".");
    fflush(stdout);
}
}
// Try again in 100ms
sleep_count++;
snooze(100);
}

for (int device_num=0;
     device_num < num_devices;
     device_num++)
{
    cleanup(device_num);
}
```

while 循环只需运行，直到每个设备都提供结果。我们设置了一个数组 processed_results[num_devices]，初始值为 false。每当某个 GPU 提供结果时，待处理结果数量就会递减，并且数组中已处理的结果会被标记，以表明该 GPU 已经提供了结果。如果任何 GPU 的结果尚未可用，CPU 线程就会休眠 100 ms，然后再次尝试。这将产生以下输出：

```
Waiting.......
ID:0 GeForce GTX 470:Copy To : 20.84 ms
ID:0 GeForce GTX 470:Kernel : 4883.16 ms
ID:0 GeForce GTX 470:Copy Back : 10.24 ms
ID:0 GeForce GTX 470:Component Time : 4914.24 ms
ID:0 GeForce GTX 470:Execution Time : 4914.24 ms
ID:0 GeForce GTX 470:Array check passed
ID:0 GeForce GTX 470:Host wait time : 5200 ms
```

```
Waiting.......
ID:3 GeForce GTX 460:Copy To : 20.58 ms
ID:3 GeForce GTX 460:Kernel : 6937.48 ms
ID:3 GeForce GTX 460:Copy Back : 10.21 ms
ID:3 GeForce GTX 460:Component Time : 6968.27 ms
ID:3 GeForce GTX 460:Execution Time : 6968.27 ms
ID:3 GeForce GTX 460:Array check passed
ID:3 GeForce GTX 460:Host wait time : 7100 ms
```

```
Waiting.......
ID:2 GeForce GTX 260:Copy To : 21.43 ms
ID:2 GeForce GTX 260:Kernel : 14269.09 ms
ID:2 GeForce GTX 260:Copy Back : 10.03 ms
ID:2 GeForce GTX 260:Component Time : 14300.55 ms
ID:2 GeForce GTX 260:Execution Time : 14300.55 ms
ID:2 GeForce GTX 260:Array check passed
ID:2 GeForce GTX 260:Host wait time : 14600 ms
```

```
Waiting.......
ID:1 GeForce 9800 GT:Copy To : 21.19 ms
ID:1 GeForce 9800 GT:Kernel : 25275.88 ms
ID:1 GeForce 9800 GT:Copy Back : 11.01 ms
ID:1 GeForce 9800 GT:Computation Time : 25308.08 ms
ID:1 GeForce 9800 GT:Execution Time : 25308.08 ms
ID:1 GeForce 9800 GT:Array check passed
ID:1 GeForce 9800 GT:Host wait time : 25300 ms
```

请注意，结果的顺序现在如预期一样。最快的设备 GTX470 只需 5 秒，而最慢的设备 9800 GT 需要 25 秒。在此期间，CPU 线程大部分时间处于空闲状态，本可以做一些有用的事情，例如在 GPU 完成任务时向它们分配更多工作。让我们看看这在实践中是如何工作的。

首先，我们需要将将工作推送到流或工作队列的任务抽象化。然后，我们可以使用它来进行初始流填充，以及在工作完成时填充流。

```
__host__ void get_and_push_work(const int num_devices,
                                const size_t single_gpu_chunk_size,
                                const u32 new_work_blocks)
{
    // Work out the total number to process
    // Number already scheduled plus new work
    u32 results_to_process = num_devices +
                             new_work_blocks;

    // Keep track of the number of calculations in flow
    u32 results_being_calculated = num_devices;

    // Keep track of how long the CPU needs to sleep
    u32 sleep_count = 0;

    // While there are results still to process
    while(results_to_process != 0)
    {
        // Process the data as it comes back from the GPUs
        // Overlaps CPU execution with GPU execution
        for (int device_num=0;
             device_num < num_devices;
             device_num++)
        {
            // Assume will process nothing
            bool processed_a_result = false;

            // If results are pending from this device
            if (processed_result[device_num] == false)
            {
                // Try to process the data from the device
                processed_result[device_num] =
                    process_result(device_num);
            }
        }
    }
    // If we were able to process the data
    if (processed_result[device_num] == true)
    {
        // Then decrease the number of pending
        // results
        results_to_process--;

        // Increment the number this device
        // processed
        num_processed[device_num]++;

        // Decrease the number in flow
        results_being_calculated--;

        // Note we processed at least
        // one result
        processed_a_result = true;

        // print the time host waited
        printf("%sHost wait time : %u ms\n",
               device_prefix[device_num],
               sleep_count * 100);

        // If there are still more blocks
        // to process
        if (results_to_process >
            results_being_calculated)
        {
            // Give more work to the
            // finished GPU
            push_work_into_queue(device_num,
                                 single_gpu_chunk_size);
        }

        // Set flag to say GPU has work
        processed_result[device_num] =
            false;

        // Increment the number of
        // active tasks
        results_being_calculated++;

        // Format output
        printf("\n");
        fflush(stdout);
    }
    // If we processed no results then sleep
    if (processed_a_result == false)
    {
        sleep_count++;
        printf(".");
        fflush(stdout);
    }

    // Try waiting in 100ms
        snooze(100);
}
}
}
```

这里，程序只是跟踪活动 GPU 任务的数量，并递减仍需处理的结果数量。当我们分配总共 64 个工作单元时，这会导致如图 8.3 所示的工作块分配给 GPU。

如您从柱状图中所见，GTX470 在相同时间内可以处理 25+ 个工作单元，而 9800 GT 只能处理 5+ 个，比例为 5:1。简单地循环并等待流同步操作会导致完全相等的工作分配，但在许多实际系统中，正如您所发现的，存在混合 GPU 的情况。许多玩家会有一张用于游戏的显卡（GTX670），然后通常还有一张较旧的显卡专门用于 PhysX（GTX260），正好构成这样的场景。事实上，较弱的显卡加在一起贡献了 37 个工作单元，比主显卡单独贡献的 27 个多出 10 个。这反过来使机器上的可用工作吞吐量增加了一倍多。

这一切很好，但我们实际上可以做得更好。我们实际上并没有充分利用系统中每个 GPU。流的设计既是为了提供流 0（默认流）的替代方案，也是为了为 GPU 提供多个工作队列。如果内核太小无法充分利用整个 GPU（这种情况不太可能），或者更常见的情况是 CPU 可能需要一些时间

![](img/e0b192dbaf05f61ad420bee512a8c4e4_302_0.png)

图 8.3 多个 GPU 的工作单元分布。

一些时间来向 GPU 提供额外工作。在我们这里的示例中，CPU 只是将数组与一组预期值进行比对，但它可能正在执行更慢的操作，例如从磁盘加载下一个工作单元。在这种情况下，我们希望 GPU 在此期间也保持忙碌。为此，我们使用一种称为双缓冲的方案。

双缓冲的工作原理是让 GPU 使用一个缓冲区，而 CPU 使用另一个缓冲区。因此，即使 CPU 正在处理一个数据集，GPU 也在执行有用的工作，而不是等待 CPU。CPU 进程可能只是简单地加载或保存磁盘上的数据。它还可能包括对来自多个 GPU 的数据进行额外处理和/或组合。

为此，我们需要根据 MAX_NUM_DEVICES 为每个数组引入另一个维度。例如：

```
// Define N streams per GPU
cudaStream_t stream[MAX_NUM_DEVICES][MAX_NUM_STREAMS];
```

然后，我们有选择支持每个设备两个或更多流。每个设备使用两个流有一个小问题，即如果我们以相同优先级向 GPU 分配工作单元，它们都会获得相同的工作单元总数。在实践中，这意味着我们最终会到达工作队列的末尾，仍在等待最慢的设备。解决方法是按 GPU 的速度比例分配工作单元。

如果您回顾图 8.3，可以看到 GT9800 是最慢的设备。GTX260 大约快两倍，GTX460 又快两倍，而 GTX470 比 GTX460 快大约 20%。鉴于我们希望至少有两个流来实现双缓冲，如果我们按设备速度比例增加分配的流数量，我们将获得一种工作分配，使所有设备在大约相同的时间内保持忙碌。我们可以使用一个简单的数组来实现这一点：

```
// Define the number of active streams per device
const u32 streams_per_device[MAX_NUM_DEVICES] =
{
10, /* GTX470 */
2, /* 9800 GTX */
4, /* GTX260 */
8, /* 460 GTX */
};
```

因此，最初我们向设备 0（GTX470）分配 10 个工作单元。然而，我们只向 GT9800 分配 2 个工作单元，依此类推。当工作单元分配完毕时，每个设备的队列长度大约为数组中显示的值。由于这大约等于相同的时间，所有设备都会在短时间内相继完成。

这里，各种 GPU 相对速度的列表是静态构建的。如果目标机器始终具有相同的硬件，那么这种方法是可行的。但是，如果您不知道目标硬件是什么，可以进行一些初始计时运行，然后在运行时完成这样的表格。需要记住的重要一点是，列表中的最小值应始终至少为 2 才能实现双缓冲。其他值应为 2 的某个倍数，反映相对于最慢设备的相对时间。

