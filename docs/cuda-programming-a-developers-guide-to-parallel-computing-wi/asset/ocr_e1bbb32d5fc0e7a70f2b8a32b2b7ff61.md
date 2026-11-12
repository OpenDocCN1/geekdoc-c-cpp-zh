```
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
memcpy_cpu_completed_data[completed_idx * MAX_OUT_QUEUED_PACKETS],
cpu_dest_data[device_num][stream_num],
chunk_size);

printf("%nProcessed work unit: %u", completed_idx);
fflush(stdout);

// Increment the destination idx
// Single array per CPU
completed_idx++;
```