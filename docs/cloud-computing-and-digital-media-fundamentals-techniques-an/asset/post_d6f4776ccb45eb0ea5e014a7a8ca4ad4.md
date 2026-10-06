
# 140 ■ Cloud Computing and Digital Media

the limitation of the network environment and support the high mobility in the pervasive learning activity so that users can have smooth learning progress. With the learning content prefetching strategy, it doesn't need to consider the speed of network and performance, because the learning activity can still be completed.

The course information, user information, and device information are saved in the learning center and learning assistant. The learning content prefetching strategy is divided into course data access module in the learning center and course prefetching module in the learning assistant because it needs to collect enough information for generating the right decision of content prefetching. Thus, this strategy is based on this information, with virtual memory management and the disk cache technical concept, and offers the best learning environment to learners.

It uses virtual memory management to solve the network problem nor the disk cache technical concept to reduce the waiting time. The basic purpose of mobile learning content prefetching strategy is to predict the learning path and, according to the learning device, pre-load the course resource. Thus, the mechanism of predicting the learning path will affect the performance of the strategy.

The learning prefetching strategy analyzes the following:

- 1. Specific relation of each learning content
- 2. Users' position information
- 3. Characteristics of the learning content
- 4. Efficacy of the mobile device

Learning center and learning assistant synchronize the learning progress by using the same course prefetching strategy. This strategy is divided into two parts: course data management module and replacement management module.

### 6.3.2.1 Course Data Management Module
This module is in the learning center, and according to the information from the learning progress recording module, it arranges the most likely part for the learner using the association table. Then it requests the learning assistant to download the file. It makes the system to pre-download these parts using idle time, which reduces the access time of network connection.

### 6.3.2.2 Replacement Management Module
Learning assistant determines the learning time by replacement management module. The parts saved in the client will not be read again and release it. Then, the modified association table is set to the learning progress recording module in the learning center to download the new parts from the course management module. Make sure that the content saved in the device has high possibility of clicked and reading rate.

## 6.3.2.2 Course Cache Strategy

Figure 6.3 shows the operating process of course cache strategy. The course cache strategy considers the related information in the replacement management module, produces the drop order for the courses, and sends this message to the learner so that they can drop these unavailable courses. Then the devices start to synchronize the changed items in the associated table to the learning center. If the learner is a new user, the value of drop order is null. When the client device has enough storage space, the learning assistant will send requests of course download. Meanwhile, the learning progress module in the server side will analyze the learning history and produce the recommended download order so that the learner may access in recent future. Then the learning center will send this download order to the assistant by the associated table, and the learning assistant can follow the associated table to download the related courses.

The accuracy of learning order prediction for learner is the main reason (Hu and Chen 2010) that may impact on the course prefetching strategy.

![](img/f13da3dd59d15874e4b22b03a274001b_163_0.png)

FIGURE 6.3 The process of course cache strategy.

## 142 ■ Cloud Computing and Digital Media

In order to have accurate information to make precise prediction, items are many reasons that should be considered. The following items are the most important reasons that may impact on the course prefetching strategy.

- Relation of course order: The course order designed by the instructor has specific reasons why the instructor designs in this order? This is one of the reasons that should be considered.
- Location of learner: The associated table has related location of learner when they access courses. Hence, the system uses geography information as one of the reasons that may impact on the strategy because different location for learner may cause different learning motivation.
- Course content: The size of course, the path length of course, and the cluster number of course.
- Devices from users: Different devices have different restriction, such as storage size and network availability.
- Learning history of learner: Course download time and last access time of learner.

## 6.3.2.2 Course Management Module

The course management module is designed in the cloud server side. The module works with the storage of learning progress module to predict the most possible course content that the learner may read in the recent future. After the prediction, the learning assistant will start to download the courses from prediction. This mechanism helps the system to download the most possible courses that the learner may read before starting the next course. It will decrease the time when the learner downloads the courses from the server, and also decrease the system access time to the Internet. With the prefetching mechanism, the system performance has an obvious improvement.

The operation in the course management module is very simple as shown in Figure 6.4. The main task of the course management module is to produce the optimal download orders by all the predicted items when it receives the request for download. After the optimization, the system will send the optimized order to the client side and provide the cluster that includes the optimized order.

![](img/f13da3dd59d15874e4b22b03a274001b_165_0.png)

FIGURE 6.4 The progress of course management module.

## 6.3.2.4 Replacement Management Module

The learning assistant services in the client side can find out the possible unavailable course content in each learning time spot and delete those unavailable course content from the user. After that, the system will download the new course content that is assigned by course management module. With this mechanism, we can confirm that all the course content in the user devices have high reading possibility. In the process of replacement management module, when the content prefetching strategy starts, this module will predict the possible content access order by a predicted factor, and then produce a drop order for learning content (Wang et al. 2011a). Meanwhile, the course management module sends the download requirement, and then gets the optimized course download order from the course management module. The system compares the drop order with the optimized course download order and removes the redundant parts, which will reduce the burden of system. For example, if the drop order is 3 and 4, the optimized course download order is 2, 5, and 3.

## 144 Cloud Computing and Digital Media

The predicted strategy will remove the item 3 from the drop list; hence, the drop order becomes 4 and the optimized course download order becomes 2 and 5. With this mechanism, it avoids the abandoned parts that will be downloaded in the recent future. After this step, the learning assistant starts to remove the content from the drop order, and the learning center starts to download the appropriate courses from the optimized course download order. In case of all the conditions that are mentioned, the system will follow the traditional rules—first in, first out (FIFO)—to remove the oldest content in the client side.

## 6.4 CONCLUSION AND FUTURE WORK

This chapter proposed a cloud-based learning center and learning assistant on the user devices to enhance the usability of pervasive learning. Except to improve the restriction to the user, it also improves the convenience of pervasive learning and provides a complete service and mechanism. The improvement satisfies the users that can learn at any time, anywhere, and any devices. During the implementation, the synchronized mechanism based on the cloud server will develop in different devices that can satisfy the requirement from the user in distance.

# ACKNOWLEDGMENTS

We thank the National Science Council. This research was supported in part by a grant from NSC 101-2221-E-240-004, Taiwan, Republic of China.

# REFERENCES

Mohammed Al-Zoube, “E-learning on the cloud,” International Arab Journal of E-Technology, 1:58–64, 2009.
Michael Arbust, Armando Fonseca, Re Griffith, Anthony D. Joseph, Randy Katz, Andy Konwinski, Gunho Lee et al., “A view of cloud computing,” Communication of ACM, 53(4):50, 2010.
Junjai Bai, Shusheng Shen, Liya Chen, and Yongsheng Zhu, Cloud learning: A new learning style; 2011 International Conference on Multimedia Technology, pp. 3460–3463, July 26–28, 2011.
Greg Boss, Padma Malladi, Dennis Quan, Linda Legregni, and Harold Hall, Cloud computing, IBM White Paper, 2007. http://download.boulder.com/ibmdl/pub/software/dw/hips/Cloud_computing_wp_final_80Oct.pdf
Michael Brock and Andrzej Goscinski, “State aware WSDL,” Sixth Australasian Symposium on Grid Computing and e-Research (AusGrid), Wollongong, NSW, pp. 35–44, January 24, 2008.
