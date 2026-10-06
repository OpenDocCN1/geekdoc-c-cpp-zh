
# Cloud-Based Intelligent Tutoring Mechanism for Pervasive Learning

Martin M. Weng
Tamkang University
New Taipei, Taiwan

Yung-Hui Chen
Lunghwa University of Science and Technology
Taoyuan, Taiwan

Neil Y. Yen
University of Aizu
Aizuwakamatsu, Japan

**+ CONTENTS**

| Section | Page |
| :--- | :--- |
| 6.1 Introduction | 128 |
| 6.2 Cloud-Based Educational Service | 131 |
| 6.3 System Architecture | 133 |
| 6.3.1 Learning Center in Cloud | 135 |
| 6.3.1.1 User Management Module | 136 |
| 6.3.1.2 Learning Progress Recording Module | 137 |
| 6.3.1.3 Course Data Access Module | 137 |
| 6.3.1.4 Course Data Management Module | 139 |
| 6.3.2 Learning Assistant in Client | 139 |
| 6.3.2.1 Course Prefetching Module (Asynchronous Cache Mechanism) | 127 |
| 6.3.2.2 Course Cache Strategy | 141 |
| 6.3.2.3 Course Management Module | 142 |
| 6.3.2.4 Replacement Management Module | 143 |
| 6.4 Conclusion and Future Work | 144 |
| Acknowledgments | 144 |
| References | 144 |

## 6.1 INTRODUCTION

“E-learning,” which is based on the Internet technology, provides a new choice different from the past—the limitation of time and space—and learners require staying together in a regulation time, for the comportment of learning. “E-learning” is a process of studying through the digital media resources for learners, and these media include the Internet, computers, satellite broadcasts, tapes, interactive TVs, and CDs. Recently, the technology of the network service in software and hardware becomes mature, and the “e-learning” industry becomes a major promoter of the movement, which says “lives old.” In response to this concept, the distance learning pattern combined with computer technology is getting more and more attention; there are many instances as the computer and multimedia technology to enumerate. But, with the development of wireless network such as WiFi, 3G, and WiMax are getting universal; the volume of mobile device is smaller than before. Therefore the use of mobile devices as smartphone is becoming the trend (Laisheng and Zheng 2011). But there are many platforms for mobile devices; if we design different platforms for each application, it will face many constraints and limits, and waste on maintenance and series of tests for different devices. With the development of Web service applications, programs transform the environment from the desktop to the Web world, which has been used many years through the Web service; users can arrange and back your list, not need to remember the settings about POP3/SMTP (Pocat and Boja 2009), and even loss of mails saved in the computer.

Moreover, no matter where you are, when you launch the Web browser, all you can do is working through Internet connection; this is the charm of Web applications (Vaquiro). This application mode is based on the cloud computing system; all the complex computing and data storage requirements are processed into the cloud server, and the client application is responsible to display the result, accept the simple operation, and increase the flexibility of use. This cloud architecture is the main trend of future application-oriented service (Armbrust et al. 2010). Using this architecture, no matter what type of smart devices users use, can easily access to these services. Cloud computing architecture can also be used in distance learning system, not just extend the use of the system from personal computer (PC) to mobile devices, whilst learning on multiple devices neither limitation conditions and device capacity. The development of any information system includes the user interface, processing logic, and data storage. The technical report of Advanced Distance Learning (ADL) divided into mutually overlapping parts.

With regard to the authoring tools of distance learning environment, it provides the editors, instructional designers, or teachers easily to design/revise the learning content, enable user to integrate an array of media to create professional, engaging and interactive learning content and also deliver the learning content to the learner easily. In the distance learning environment, the learning learning content or materials follow some international standards or specifications to develop, and these usually focus on defining the level of architecture rather than the content (Tu and Chen 2011). Emphasizing on sharing and exchanging of the information era, the teacher must realize the process of using authoring tool to construct a course, the difficulty will become the number killer of traditional teaching. Thus, another purpose of the authoring tools is to assist the author or instructional designer packaging the learning content corresponding to the international standards (SCORM, Wu et al. 2011), Industry Computer-Based Training (CBT) Committee (AICC), instructional management system (IMS) Question and test interoperability (QTI), or IMS Common Cartridge (CC).

LMS not only provides courses, manages the learner and user, and maintains learning record, but also acts the role of the display platform of the learning component produced by authoring tool mentioned earlier. Therefore, collecting the user information is quite important for further analysis, provide the author share the course, learning portfolio, record, and through the distributed learning systems to break the information exchange problem in the individual digital learning platform, allow the user to use one learning system and to the different courses or information from the other systems. The storage is the platform to collect and store the learning component, the system that stores the course component and provides the function as research, publish, import, and export is called repository system. This research is based on the rich computing resource of cloud environment, aims to assist pervasive learning, and develops the core mechanism and related service. We use the HTML5 standard and Android operations systems to develop; escaping the dilemma of previous product development is limited by the terminal device.

The purpose of this research and its results are as follows:

- 1. Combination of the concept of cloud computing "anytime, anywhere, and any device" and smart device system develops a distance learning system that can remote use at any time. This system applies the SCORM and CC standards; compatible with other distance learning system, it applies the same standards and extends the applications from PCs to the mobile devices as smartphone or tablet PC. The system of this research developed is fully using the mobility, execution, and touch screen interaction interface of the smartphone; when learner uses this system, it is based on the learner's demands and learning progress to access the learning resources on the cloud server and start the distance learning.
- 2. Learners are able to download the learning content to the handheld device and then learn offline without the Internet connection. The learner should connect to the cloud server when he or she needs to update or synchronize the learning progress. The system will determine the most need for course synchronization automatically and decrease the size of file transmission. Through the cloud service, the learner can upload and synchronize the learning progress to the cloud server and continue the learning activity on the other devices. For example, the learner can download the course from the cloud server to the smartphone and learn in the commuting time; after the learner enters into the classroom, the device will automatically update the learning progress to the cloud server, and switch the learning platform to the PC and restart the learning.
