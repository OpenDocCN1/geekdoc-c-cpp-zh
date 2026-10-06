# Video Transcode Scheduling for MPEG-DASH in Cloud Environments ■ 111

the requirements of the computing-intensive and time-consuming video transcoding jobs.

+   - Cost: The biggest advantage of cloud computing is the elimination of the investment in stand-alone software or servers by the user. With cloud computing, there are no separate overhead charges as cost of data storage, software updates, management, and most importantly cost of quality control. Currently, anyone can use the services of cloud computing at affordable rates. In our case, video segments can be encoded within a fairly short time after being uploaded to the server by spending a small amount of money.

# 5.2.1 Existing Cloud Video Transcoding Service

There exist several commercial cloud services that support video transcoding.

+   - Amazon released their Elastic Transcoder [11] in January 2013. Amazon Elastic Transcoder manages aspects of the transcoding process transparently and automatically. It also enables customers to process multiple files in parallel and organize their transcoding workflow using a feature called transcoding pipelines. With Amazon Elastic Transcoder's pipeline feature, customers set up pipelines for these various scenarios and ensure that their files are encoded when how they want, allowing them to seamlessly scale for spiky workloads efficiently. It runs the transcoding jobs using Amazon Elastic Compute Cloud (Amazon EC2) [12] and stores the video content in the Amazon Simple Storage Service (Amazon S3) [13]. Developers can simply use the Web-based console or application programming interfaces (APIs) to create a transcoding job that specifies an input file, the transcoding settings, and the output file. They can also assign the priority of each pipeline to allow important videos to be encoded first. Amazon charges a video transcoding fee according to the output duration and definition.

+   - Zencoder [14] provides video transcoding services as well. In addition to providing typical video transcoding services in the cloud, it also supports live video transcoding. Its Web service accepts Real-Time Messaging Protocol (RTMP) input streams and encodes to RTMP and HLS at multiple bit rates for adaptive bit rate playback. Zencoder provides different price packages so that users can select the most appropriate one on their own video duration and definition.