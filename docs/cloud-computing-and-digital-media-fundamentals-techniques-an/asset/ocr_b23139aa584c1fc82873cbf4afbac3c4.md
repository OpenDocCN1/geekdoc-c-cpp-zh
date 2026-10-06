# 11.3.2 Open-Source Cloud Framework—Hadoop

Although Google has revealed the design of its cloud computing infrastructure, the implementation of its system still keeps in secret. Then we come to the famous open-source cloud computing framework—Hadoop. Apache Hadoop is a Java software framework that supports data-intensive distributed applications under a free license. It enables applications to work with thousands of nodes and petabytes of data. Since Hadoop was inspired by Google's MapReduce and GFS paper, the basic knowledge of GFS and MapReduce model introduced in Section 11.3.1 also works well in Hadoop. In Hadoop framework, Hadoop distributed file system (HDFS) is the open-source implementation of GFS and Hadoop also implements the MapReduce model.

Even the version of Hadoop is 0.20.2, which is still far from 1.0, a variety of companies and organizations use Hadoop for production, as Adobe that uses Hadoop and HBase in several areas from social services to structured data and processing for internal use; Amazon Web Service provides a hosted Hadoop framework running on the Web-infrastructure of Amazon Elastic Compute Cloud (Amazon EC2) and Amazon Simple Storage Service (Amazon S3) and Facebook that uses Hadoop to store copies of internal log and data sources and use it as a source for reporting/analytics and machine learning.

In addition, many researchers have extended Hadoop framework for scientific purposes. In Reference 13, a technique is applied to binary image files in order to enable Hadoop to implement image processing techniques on a large scale. Bortnikov [14] shows how Hadoop can be applied for Web-scale computing. He et al. [15] design and implement a MapReduce framework on graphics processors.

In this section, we mainly discuss the Hadoop MapReduce implementation and introduce the MapReduce user interfaces.

# 11.3.2.1 Overview of Hadoop MapReduce

In Hadoop, a MapReduce usually splits the input dataset into independent chunks, which are processed by the map tasks in a completely parallel manner. The framework sorts the outputs of the maps, which are then input to the reduce tasks. Typically, both the input and the output of the job are stored in a file system. The framework takes care of scheduling tasks, monitors them, and reexecutes the failed tasks.

The MapReduce framework consists of a single master JobTracker and one slave TaskTracker per cluster node. The master is responsible for