| Module | CPU Time |
|---|---|
| libiomp5.so | 5.52 |
| vmlinux | 0.45 |
| FLANN::searchLevel | 0.08 |
| FLANN::meanSplit | 0.06 |

(a)

| Module | CPU Time |
|---|---|
| libiomp5.so | 1.03 |
| FLANN::meanSplit | 0.66 |
| FLANN::searchLevel | 0.58 |
| FLANN::selectDivision | 0.93 |

(b)

```
flann::NNIndex<flann::L2<float>>::knnSearch          libiomp5.so
flann_find_nearest_neighbors_index                    libflann.so.1.8.4
flann_find_nearest_neighbors_index<float, float>      libflann.so.1.8.4
flann_find_nearest_neighbors_index                    libflann.so.1.8.4
call_flannC                                           server
call_image_matching_module                            server
clone                                                 libc-2.12.so
```

(c)

![](bbox=[0.13, 0.44, 0.82, 0.6])

(d)

|  |  |  |  |
|---|---|---|---|
| ▶ kmpc_global_thread_num | 27.350s | 24.537s libiomp5.so |  |
| ▶ _kmp_fork_call | 9.109s | 9.109s libiomp5.so |  |
| ▶ flann::KDTreeIndex<flann::L2<float>>::search | 1.701s | 0s libflann.so.1.8.4 |  |
| ▶ flann::KDTreeIndex<flann::L2<float>>::mean | 0.300s | 0s libflann.so.1.8.4 |  |
| ▶ std::_adjust_heap<__gnu_cxx::__normal_iter | 0.090s | 0s libflann.so.1.8.4 |  |
| ▶ flann::KDTreeIndex<flann::L2<float>>::select | 0.040s | 0s libflann.so.1.8.4 |  |
| ▶ flann::KNNSimpleResultSet<float>::addPoint | 0.030s | 0s libflann.so.1.8.4 |  |

(e)

# FIGURE 11.13

VTune analysis when using 120 DBThreads and 2 FLANN Threads in a database of 800 images. (a) hotspots 120 DBThreads, (b) hotspots 2 FLANN Threads, (c) lock and wait times with DBThreads, (d) CPU utilization by thread with FLANN threads, (e) CPU utilization by modules with FLANN threads.