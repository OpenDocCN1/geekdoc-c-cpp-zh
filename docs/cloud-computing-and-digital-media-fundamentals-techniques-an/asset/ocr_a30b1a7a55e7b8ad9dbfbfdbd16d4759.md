# Cloud-Based Intelligent Tutoring Mechanism for Pervasive Learning ■ 139

separated file will be compressed by the zip file, and the learning assistant will restore the course when it receives all the zip files. After that, every file will be identified by its sum attribute. The learning assistant will check the Checksum attribute to confirm the course files just downloaded are correct.

# 6.3.1.4 Course Data Management Module

This module is responsible for managing the course data and recording the relations between the course data. The relations include the priority of the course and the connections. For example, course A is the leading course of course B. This module shows the dependencies of these two courses. According to this relation, the teacher can control the learning progress by adding, modifying, and deleting the course file, and decide which account can access the course by the user management module. This module combined with the course prefetching module in the learning assistant is mainly responsible for the entire course prefetching strategy of this research.

# 6.3.2 Learning Assistant in Client

Learning assistant is an important tool that the user uses in his or her devices. With the connection between learning assistant and learning center, the learner can download the related courses on their devices and synchronize their learning progress to the learning center. The course prefetching module is the most important module in learning assistant.

# 6.3.2.1 Course Prefetching Module (Asynchronous Cache Mechanism)

Since large amounts of multimedia material will be applied to the course files in this research, the execution performance of the smart device and the status of the network connection will affect the learning fluency. When the learner is learning in an outdoor environment, or he often encounters this situation. For example, if the learning activity needs a large size file, the learner will spend much time waiting for the transmission to complete, and the learner does not necessarily stay in a permanent network environment. This situation will cause the interruption of learning. Thus, this module will construct an automatic learning content prefetching strategy, coordinate with the “course data management module” in the learning center, allow the learning assistant to predownload the course file that the learners need, reduce the interruption and unnecessary time of waiting, and help the learners to learn smoothly.

Learning content prefetching strategy is an automatic mechanism for the mobile network environment. The purpose of this strategy is to conquer