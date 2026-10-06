# 28 Cloud Computing and Digital Media

Multimedia cloud data center

![](bbox=[0.136, 0.126, 0.863, 0.513])

FIGURE 2.1 Data center architecture for multimedia applications.

back to the users by the transmission server. In practical cloud platforms, such as Amazon EC2 [5] or Windows Azure [28], the bandwidth resource is specified by the total transmission amount. Therefore, we use the allocated bandwidth to represent the resource of the transmission server. The computing servers and the transmission server share results in the memory, and thus, there is no delay between computing servers and the transmission server in our data center architecture. Owing to the time-varying workload, the resources in the cloud have to be dynamically adjusted. Therefore, we divide the domain into time slots with a fixed length Γ. In our work, the cloud resources will be dynamically allocated in every time slot t.

According to different usages, there are two types of cloud: storage-oriented cloud, such as Amazon Simple Storage Service (Amazon S3) [29], and computation-oriented cloud, such as Amazon EC2 [5]. In this chapter, we study the computation-oriented cloud. The allocated cloud resources in our study include the scheduling resource, the computation resource,