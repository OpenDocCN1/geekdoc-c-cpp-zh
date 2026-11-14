
![](img/55beb9162c0073b3a3d7b44f1d5873e8_12_0.png)

FIG. 1.1 Block diagram of a typical embedded computing system.

## 1.2 EMBEDDED SYSTEMS IN SOCIETY AND INDUSTRY

While not necessarily comprehensive, Fig. 1.2 illustrates the diversity of the domains and environments in which embedded systems operate. At home, embedded systems are used to control and monitor our appliances from the simple stand-alone microwave oven, washing machine, and thermostat, to the more sophisticated and sensitive security system that monitors cameras and possibly communicates with remote systems via the Internet. Embedded systems also control our vehicles from the fuel injection control to the monitoring of emissions while managing a plethora of information using visual aids to display the operation of our vehicles. In our cities, embedded systems monitor public transportation systems which are ubiquitously connected to central stations performing online scheduling of buses and trains and provide real-time updates of arrival times across all stops for all transportation lines. At the office, embedded systems handle small electronic devices such as printers, cameras, and security systems as well as lighting.

Moreover, today's smartphones are a marvel of technological integration and software development. These high-end embedded systems now include multicore processor(s), WiFi, Bluetooth, touch screens, and have performance commensurate to the performance of high-end multiprocessing systems available just a few years ago to solve scientific and engineering computing problems.

![](img/55beb9162c0073b3a3d7b44f1d5873e8_13_0.png)

## 1.3 EMBEDDED COMPUTING TRENDS

Over the last decades, the seemingly limitless availability of transistors has enabled the development of impressive computing architectures with a variety and heterogeneity of devices. This resulted in the ability to combine, on a single integrated circuit, computing and storage capacity, previously unimaginable in terms of raw hardware performance and consequently in terms of software complexity and functionality. Various empirical laws have highlighted and captured important trends and are still relevant today in the context of embedded systems. These empirical laws include:

- Moore's Law—"The number of components in integrated circuits doubles every 18 months." Moore's Law is one of the driving forces leading to the miniaturization of electronic components and to their increasing complexity;
- Gustafson's Law—"Any sufficiently large problem can be efficiently parallelized." Due to the increasing complexity of embedded applications, the potential to use the many- and multicore architectures has also increased;
- Wirth's Law—"Software gets slower faster than hardware gets faster." This observation is supported by the fast advances of multicore systems and custom computing and hardware accelerators when compared with the availability of effective development tools and APIs (Application Programming Interfaces) to exploit the target architectures;
- Gilder's Law—"Bandwidth grows at least three times faster than computer power." This observation points to the advances in data transmission which amplify the advances of computing and storage technologies, forming the basis of technologies such as cloud computing and the Internet of Things (IoT).

One of the key trends in embedded systems has been the growing reliance on multi-core heterogeneous architectures to support computationally intensive applications while ensuring long battery lifetimes. This increase in computing power coupled with the ever increase desire to be connected has fueled a fundamental transition from embedded systems, mostly operating in stand-alone environments, to a context where they are ubiquitously connected to other devices and communication infrastructures, in what has been coined as the Internet of Things (IoT).

As with the evolution of hardware, IoT software requirements have also evolved to support more application domains. While in the past years, the focus has been on digital signal and image processing, embedded systems are now expected to interact with other devices on the network and to support a variety of applications, e.g., with the capability to search remote databases and to compute using geographically distributed data.

Not surprisingly, the computational demands of mobile applications have also increased exponentially [2], thus exacerbating the complexity of mapping these applications to mobile architectures. It is believed (see, e.g., [3]) that in some domains neither hardware scaling nor hardware replication is enough to satisfy the performance requirements of advanced mobile applications. Therefore, in addition to the research and development of next-generation hardware architectures, it will be critical to revisit the development and mapping process of applications on resource-constrained devices. In particular, a key step ahead, when considering algorithmic and/or target hardware system changes, is the evaluation of code transformations and compiler optimizations that fully leverage the acceleration capabilities of the target system.

Another critical issue for companies is time-to-market [4] (see Fig. 1.3). Delays entering the market mean smaller overall sales as products have less time to benefit from the market before it starts to decline. Thus, a fast and efficient process to develop applications is one of the key factors for success in such competitive markets.

## 1.4 EMBEDDED SYSTEMS: PROTOTYPING AND PRODUCTION

Fig. 1.4 illustrates a design flow for embedded systems. Developing a high-performance application for an embedded platform requires developers to exploit sophisticated tool flows and to master different levels of abstraction across the various stages of application development, including deployment and maintenance.

![](img/55beb9162c0073b3a3d7b44f1d5873e8_15_0.png)

FIG. 1.3 Simplified sales model and marketing entry.

Based on Vahid F, Givargis T. Embedded system design: a unified hardware/software introduction. 1st ed. New York, NY: John Wiley & Sons, Inc.; 2001.

In our example, the development flow begins by capturing the user requirements followed by the actual development of the application. A first proof-of-concept prototype is usually validated on a desktop computer, possibly using a programming language with features that facilitate early prototyping such as MATLAB, and relying on the emulation of external interfaces (e.g., instead of using the real camera, one can use prerecorded videos or simple sequences of images stored as files). If this initial prototype does not meet its functional requirements, the developer must iterate and modify the application, possibly changing its data types (e.g., converting double to single floating-point precision), and applying code transformations and/or refactoring code to meet the desired requirements. This process is guided by developers’ knowledge about the impact of these modifications on the final embedded version. Depending on the project at hand, the prototype may be developed in the same programming language used for the embedded version, but possibly using different APIs.

The next step of the development process involves modifying the prototype code to derive an embedded code implementation. This includes using emulators, simulators, and/or virtual platforms to validate the embedded version and to optimize it if needed. At this stage, developers must consider the full set of nonfunctional requirements. It is also typical at this stage to explore and test hardware accelerators. This step partitions and maps the selected computations to available accelerators. If this validation stage is successful, the application is then deployed to the target embedded system or to a hardware system emulator, and a second stage of validation is

![](img/55beb9162c0073b3a3d7b44f1d5873e8_16_0.png)

FIG. 1.4 An example of a design flow for developing an embedded application.
