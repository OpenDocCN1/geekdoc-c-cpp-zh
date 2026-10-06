
# Mobile Multimedia Cloud Computing ■ 11

TABLE 1.4. Architecture Designed in Recent Studies toward Mobile Multimedia Computing

| Architecture | Brief Description |
| --- | --- |
| i5Cloud architecture [2] | It consists of four layers of infrastructure, platform, multimedia services, and application. |
| Cloud mobile media architecture [2] | It is capable of dynamically rendering multimedia in the cloud servers, depending on the mobile network and cloud computing constraints. |
| Multimedia streaming service over cloud computing [16] | It provides dynamic streaming services while considering mobile device resources, multimedia codec characteristics, and the current network environment. |
| Multimedia cloud computing [3] | It provides multimedia applications and services over the Internet with desired QoS. |

| Application layer | Collaborative documentation in cultural heritage | Intelligent mobile media with cloud services |
| Multimedia service layer | Collaborative multimedia services | Semantic metadata services | Video services | Transcoding |

(Note: The text above contains "Multimedia service layer | Collaborative multimedia services | Semantic metadata services Video services Transcoding")

FIGURE 1.2 i5Cloud architecture for multimedia applications. ROI, region-of-interest.

EC2. The DeltaCloud core framework assists in creating intermediaries that interpret the DeltaCloud representational state transfer (REST) API on the front while communicating with cloud providers using their own native APIs on the back. The concurrent editing and multimedia sharing components are the engine for the collaborative multimedia and semantic metadata services. MPEG-7 metadata standards are employed to realize semantic metadata services. Video processing

# 12 Cloud Computing and Digital Media

Internet cloud Core network Radio access network Mobile clients

![](img/f13da3dd59d15874e4b22b03a274001b_34_0.png)

Figure 1.3 Cloud mobile multimedia architecture with control and data flows. PGW, packet data gateway; SGW, service gateway. (From Wang, S. and Dey, S., IEEE Transactions on Multimedia, 99, 1, 2013. With permission.)

services improve mobile users’ experience. The application layer provides a set of services for mobile users to create multimedia to collaboratively annotate and share.

Wang et al. [1] described a typical architecture for cloud mobile multimedia applications, including end-to-end flow of control and data between the mobile devices and the Internet cloud servers (Figure 1.3). A typical cloud multimedia application primarily relies on cloud computing IaaS and SaaS services in public, private, or hybrid clouds. A multimedia application has a thin client on mobile devices, which provides the appropriate user interfaces (gesture, touch screen, voice, and text based) to enable users to interact with the application. The resulting control commands are transmitted uplink through cellular access network (RAN) or WiFi access points to appropriate gateways in an operator core network (CN) and finally to the cloud. The content produced by the multimedia cloud service is transmitted downlink through the CN and RAN back to the mobile device. Then the client decodes and displays the content on the mobile device display.

To address the restricted bandwidth and improve the quality of multimedia video playback, Chang et al. [16] proposed a novel cloud multimedia streaming architecture for providing adjustable streaming services (Figure 1.4), which consist of two parts: the service function of the cloud equipment (i.e., cloud service) and the information modules provided by the mobile device (i.e., mobile device service). Table 1.5 describes the architecture modules.

![](img/f13da3dd59d15874e4b22b03a274001b_35_0.png)

FIGURE 1.4 Multimedia streaming service architecture over cloud computing. OS, operating system. DYNAMIC, adaptive streaming; LCD, liquid-crystal display. (From Chang, S., Lai, C., and Huang, Y., *Computer Communications*, 35, 1798–2012. With permission.)

TABLE 1.5 Module Description for the Multimedia Streaming Service Architecture

| Module | Sub-Module | Description |
|---|---|---|
| Cloud service | Device profile management | Records the features of multimedia devices as the maximum power of the processor, the codec type, the available highest speed of the network, and the highest available download speed of the network |
| | Policy evaluation module | Determines the multimedia coding parameters, in terms of mobile device parameters |
| | Multimedia storage cloud | Provided by some multimedia storage devices |
| Mobile device service | Register system | Registers a device profile over the cloud |
| | Notification system | Has the hardware monitor and notification component, which is used to monitor the real-time information of battery and network bandwidth |
| | Examination sampling system | Measures system efficiency, including the parameters in the DPM* |
| | Playback system | Parses metadata to obtain film coding characteristics and relevant information |
| | Control and configuration system | Offers user-machine interface interaction settings and controls hardware module functions |

* DPM, device profile manager.

FIGURE 1.5 Architecture of multimedia cloud computing: Media cloud (a) and cloud media (b) services. (From Zhu, W., Lu, C., Wang, J., and Li, S., “Multimedia Cloud Computing,” IEEE Signal Processing Magazine, 28, 59–69, 2011. ©2011 IEEE.)

It is foreseen that cloud computing could become a disruptive technology for mobile multimedia applications and services [18]. In order to meet multimedia's QoS requirements in cloud computing for multimedia services over the Internet and mobile wireless networks, Zhu et al. [3] proposed a multimedia cloud computing framework that leverages cloud computing to provide multimedia applications and services over the Internet. The principal conceptual architecture is shown in Figure 1.5. Zhu et al. addressed multimedia cloud computing from multimedia-aware cloud (media cloud) and cloud-aware multimedia (cloud media) perspectives. The media cloud focuses on how a cloud can perform distributed multimedia processing and storage and QoS provisioning for multimedia services. In a media cloud, the storage, CPU, and GPU, are presented at the edge (i.e., MEC) to provide distributed parallel processing and QoS adaptation for various types of devices. The MEC stores, processes, and transmits data at the edge, achieving a shorter delay. In this way, the media cloud, composed of MECs, can be managed in a centralized or peer-to-peer (P2P) manner. The media cloud (Figure 1.5b) focuses on how multimedia services and applications, such as storage and sharing, authoring and mashup, adaptation and delivery, and rendering and retrieval, can optimally utilize cloud resources to achieve better quality of experience (QoE). As depicted in Figure 1.5b, the media cloud provides raw resources, such as hard disk, CPU, and GPU, rented by the media service providers (MSPs) to serve users. MSPs use media cloud resources to develop multimedia applications and services, for example, storage, editing, streaming, and delivery.

![](img/f13da3dd59d15874e4b22b03a274001b_36_0.png)

# 1.5 OVERVIEW OF MULTIMEDIA CLOUD SERVICES

Mobile multimedia cloud computing presents a significant technology to provide multimedia services to generate, edit, process, and search multimedia contents via the cloud and mobile devices. Traditionally, there exist different types of multimedia services, such as photo sharing searching and editing, multimedia streaming, image searching and rendering, and multimedia content delivery. A typical multimedia life cycle is composed of acquisition, storage, processing, dissemination, and presentation [3]. Theoretically, this section presents multimedia cloud services examined by the recent studies (Table 1.6).

Cloud multimedia authoring as a service [3] is the process of editing multimedia contents, whereas a mashup dealing with multiple segments from different multimedia sources. Cloud can make online authoring and mashup very effective, providing more functions to clients, since it has powerful computation and storage resources that are widely distributed geographically. Cloud multimedia authoring can avoid the preinstallation of an authoring software in clients. With the use of the cloud multimedia authoring service, users editing in the media cloud. One of the key challenges in cloud multimedia authoring is the computing and communication costs in processing multiple segments from single or multiple sources. Zhu et al. [3] pointed out that future research needs to tackle distributed storage and processing in the cloud, online previewing on mobile devices.

Cloud multimedia storing as a service is a model of networked online storage where multimedia content is stored in virtualized pools of storage.

# TABLE 1.6 Multimedia Cloud Services Examined by the Recent Studies

| Service | Description |
|---|---|
| Cloud multimedia authoring | The process of editing segments of multimedia contents in the media cloud |
| Cloud storage | The advantage of being "always-on," higher level of reliability than local storage |
| Cloud multimedia rendering | Conducting multimedia rendering in the cloud, instead of the mobile device |
| Cloud multimedia streaming | Potentially achieving a lower latency and providing much a higher bandwidth due to a large number of servers deployed in the cloud |
| Cloud multimedia adaptation | Conducting both offline and online media adaptation to different types of terminals |
| Cloud multimedia retrieval | Achieving a higher search quality with acceptable computation time, resulting in better performance |
