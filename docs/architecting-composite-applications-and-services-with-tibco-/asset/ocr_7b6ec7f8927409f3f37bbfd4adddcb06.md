data structures had to be increased to 100 KB. Showing the actual network interface card (NIC) bandwidth on the graph makes it even clearer that the bandwidth limit has been reached. Note that in this case the operating capacity is now lower than before.

There is an important lesson in this example regarding test harness and component parameters: The settings of these parameters can alter the apparent capacity of the component under test, often erroneously. In this case, the test never reached the operating capacity of the component under test. Instead, it ran into what might be best described as a test harness limitation: It ran out of network bandwidth.

On numerous occasions TIBCO customers have reported supposedly poor benchmark results with Enterprise Message Service only to discover upon investigation that they had run into a network bandwidth limitation such as a 10 Mbit or 100 Mbit NIC card or switch. This is why it is so important to graph resource utilization in these benchmark tests so that you really understand the nature of the limit you have encountered.

# Identifying Disk Performance Limits

Identifying disk performance limits is complex, for a variety of reasons. Nevertheless, it is an important consideration. As with network bandwidth, it is not practical in most environments to measure disk access. You have to work with computations—estimates.

Disk performance shows up in a variety of guises. The obvious cases are file operations being performed by the component. A bit less obvious are the database accesses. If you have appropriate benchmarks for the database that reflect your component’s usage patterns, you can use those. However, if you are designing your own database you may have to do your own benchmark or, failing that, your own estimates.

There are two different types of measurements that are relevant to disk access. One is the rate at which requests for disk access occur, which is commonly measured in terms of I/O operations per second (IOPS). The other is the rate at which data is being transferred to and from the disk, commonly referred to as the disk data transfer rate and is measured in bytes/second.

It also makes a difference whether the component is reading or writing to the disk: Read requests can be answered from a cached buffer, so you need some estimate as to the likelihood that the result you are looking for is already in the cache. Write performance depends upon the writing strategy: synchronous or asynchronous. Synchronous