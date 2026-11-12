

snooze(100);
}

// Print summary of how many each device processed
for (u32 device_num=0u;
     device_num < num_devices;
     device_num++)
{
    printf("%s processed: %u",
           device_prefix[device_num],
           num_processed[device_num]);
}

printf("\nTotal: src:%u dst:%u",
       unprocessed_idx, completed_idx);

cleanup_devices(num_devices);
}

客户端代码在从服务器接收初始工作并生成 GPU 工作队列后，会运行一个循环直到工作完成。该循环将工作分发给可用的 GPU，处理已完成的工作，并将任何已完成的工作发布到服务器。最后，如果无法执行上述任何操作，它将休眠 100 ms 然后重试。程序退出时，我们会打印每个设备处理的工作单元数量摘要。

请注意，调度方式与之前的示例不同。我们现在需要一些额外的缓冲区空间来将已完成的单元发布到服务器，并留出一些时间将数据推入传输队列。因此，我们不再立即将工作重新调度到 GPU，而是稍后安排额外的工作。这允许采用更简单的方法：分发工作，收集任何已完成的工作，如有必要在本地处理，然后将其发布到服务器。

```
__host__ u32 distribute_work(const int num_devices,
                             const size_t chunk_size,
                             u32 pending_results)
{
    u32 work_units_scheduled = 0;

    // Cycle through each device
    for (u32 device_num = 0;
         device_num < num_devices;
         device_num++)
    {
        u32 stream_num = 0;
        bool allocated_work = false;

        while ((allocated_work == false) &&
               (stream_num < streams_per_device[device_num]))
        {
            // If there is more work to schedule
            if (pending_results > 0)
            {
                // If the device is available
                if (processed_result[device_num][stream_num] == true)
                {
                    // Allocate a job to the GPU
                    push_work_into_queue(device_num,
                                         chunk_size,
                                         stream_num);
                    // Set flag to say GPU has work pending
                    processed_result[device_num][stream_num] = false;
                    // Keep track of how many new
                    // units were issued
                    work_units_scheduled++;
                    // Move onto next device
                    allocated_work = true;
                }
                pending_results--;
            }
            stream_num++;
        }
    }
    return work_units_scheduled;
}
```

在这里，我们遍历 processed_results 数组，以查看流中的任何元素在上一个周期中是否已处理，现在是否可以再次使用。然后我们分配待处理的工作，使得每个 GPU 设备将一个工作单元分配到可用的流槽中。

```
__host__ void push_work_into_queue(const u32 device_num,
                                   const size_t chunk_size,
                                   const u32 stream_num)
{
    // No dynamic allocation of shared memory required
    const int shared_memory_usage = 0;
    // Define the number of threads and blocks to launch
    const int num_threads = 256;
    const int num_blocks = ((NUM_ELEM + (num_threads - 1)) / num_threads);
    // Copy in the source data from the host queue
    memcpy(cpu_src_data[device_num][stream_num],
           cpu_unprocessed_data[unprocessed_idx % MAX_IN_QUEUED_PACKETS],
           chunk_size);

    // Processed this packet
    unprocessed_idx++;

    // Select the correct device
    CUDA_CALL(cudaSetDevice(device_num));

    // Push the start event into the stream
    CUDA_CALL(cudaEventRecord(memcpy_to_start_event[device_num][stream_num],
                              stream[device_num][stream_num]));

    // Copy a chunk of data from the CPU to the GPU
    // asynchronous
    CUDA_CALL(cudaMemcpyAsync(gpu_data[device_num][stream_num],
                              cpu_src_data[device_num][stream_num],
                              chunk_size,
                              cudaMemcpyHostToDevice,
                              stream[device_num][stream_num]));

    // Push the start event into the stream
    CUDA_CALL(cudaEventRecord(kernel_start_event[device_num][stream_num],
                              stream[device_num][stream_num]));

    // Invoke the GPU kernel using the newly created
    // stream - asynchronous invocation
    gpu_test_kernel<<<num_blocks,
                      num_threads,
                      shared_memory_usage,
                      stream[device_num][stream_num]>>>
                      (gpu_data[device_num][stream_num],
                       kernel_iter);

    cuda_error_check("Failed to invoke gpu_test_kernel");

    // Push the start event into the stream
    CUDA_CALL(cudaEventRecord(memcpy_from_start_event[device_num][stream_num],
                              stream[device_num][stream_num]));

    // Copy a chunk of data from the GPU to the CPU
    // asynchronous
    CUDA_CALL(cudaMemcpyAsync(cpu_dest_data[device_num][stream_num],
                              gpu_data[device_num][stream_num],
                              single_gpu_chunk_size,
                              cudaMemcpyDeviceToHost,
                              stream[device_num][stream_num]));

    // Push the stop event into the stream
    CUDA_CALL(cudaEventRecord(memcpy_from_stop_event[device_num][stream_num],
                              stream[device_num][stream_num]));
}
```

push_work_into_stream 函数与之前大致相同。不过，它现在接受一个 stream_num 参数，允许我们填充流中的任何可用槽位。它还从 cpu_unprocessed_data（CPU 主机侧常规内存数组）将数据复制到 CPU 内存中。请注意，这不是 GPU 异步内存操作使用的页映射主机内存。CPU 主机需要能够根据需要自由计算/更新此内存，而无需担心与正在进行的 GPU 内核同步。

```
__host__ u32 collect_work(const int num_devices,
                          const size_t chunk_size)
{
    // Keep track of the number of results processed
    u32 results_processed = 0;

    // Cycle through each device
    for (u32 device_num = 0;
         device_num < num_devices;
         device_num++)
    {
        // Then cycle through streams
        for (u32 stream_num = 0;
             stream_num < streams_per_device[device_num];
             stream_num++)
        {
            // If results are pending from this device
            if (processed_result[device_num][stream_num] == false)
            {
                // Try to process the data from the device
                processed_result[device_num][stream_num] = process_result(device_num,
                                                                          stream_num,
                                                                          chunk_size);

                // If we were able to process the data
                if (processed_result[device_num][stream_num] == true)
                {
                    // Increment the number this device
                    // processed
                    num_processed[device_num]++;

                    // Increment this run's count
                    results_processed++;
                }
            }
        }
    }
    return results_processed;
}
```

collect_result 函数只需遍历所有设备及其每个流，并调用 process_result 函数来尝试处理任何可用的结果。

```
__host__ bool process_result(const u32 device_num,
                             const u32 stream_num,
                             const size_t chunk_size)
{
    bool result;
    bool stop_event_hit = (cudaEventQuery(memcpy_from_stop_event[device_num][stream_num])
                           == cudaSuccess);
    // Space is available if network_out_idx is not
    // more than the total queue length behind
    bool output_space_avail = ((completed_idx - network_out_idx) <
                               MAX_OUT_QUEUED_PACKETS);
    // If the stop event has been hit AND
    // we have room in the output queue
    if (stop_event_hit && output_space_avail)
    {
        float time_copy_to_ms = 0.0F;
        float time_copy_from_ms = 0.0F;
        float time_kernel_ms = 0.0F;
        float time_exec_ms = 0.0F;
        // Select the correct device
        CUDA_CALL(cudaSetDevice(device_num));
        // Get the elapsed time between the copy
        // and kernel start
        CUDA_CALL(cudaEventElapsedTime(&time_copy_to_ms,
                                       memcpy_to_start_event[device_num][stream_num],
                                       kernel_start_event[device_num][stream_num]));
        // Get the elapsed time between the kernel start
        // and copy back start
        CUDA_CALL(cudaEventElapsedTime(&time_kernel_ms,
                                       kernel_start_event[device_num][stream_num],
                                       memcpy_from_start_event[device_num][stream_num]));
        // Get the elapsed time between the copy back start
        // and copy back start
        CUDA_CALL(cudaEventElapsedTime(&time_copy_from_ms,
                                       memcpy_from_start_event[device_num][stream_num],
                                       memcpy_from_stop_event[device_num][stream_num]));
        // Get the elapsed time between the overall start
        // and stop events
        CUDA_CALL(cudaEventElapsedTime(&time_exec_ms,
                                       memcpy_to_start_event[device_num][stream_num],
                                       memcpy_from_stop_event[device_num][stream_num]));

        // Print the elapsed time
        const float gpu_time = (time_copy_to_ms +
                                time_kernel_ms +
                                time_copy_from_ms);

        printf("%sCopy To : %.2f ms",
               device_prefix[device_num], time_copy_to_ms);

        printf("%sKernel : %.2f ms",
               device_prefix[device_num], time_kernel_ms);

        printf("%sCopy Back : %.2f ms",
               device_prefix[device_num],
               time_copy_from_ms);

        printf("%sComponent Time : %.2f ms",
               device_prefix[device_num], gpu_time);

        printf("%sExecution Time : %.2f ms",
               device_prefix[device_num], time_exec_ms);
        fflush(stdout);

        // Data has now arrived in
        // cpu_dest_data[device_num]
        check_array(device_prefix[device_num],
                    cpu_dest_data[device_num][stream_num],
                    NUM_ELEM);

        // Copy results into completed work queue
        memcpy(&cpu_completed_data[completed_idx * MAX_OUT_QUEUED_PACKETS],
               cpu_dest_data[device_num][stream_num],
               chunk_size);

        printf("\nProcessed work unit: %u", completed_idx);
        fflush(stdout);

        // Increment the destination idx
        // Single array per CPU
        completed_idx++;
    }
}
```

