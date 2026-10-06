

## 专业社区中的支持实践 ■ 75

分区决策是根据云端和设备的输入作为优化问题完成的，例如 CPU 负载、可用内存、设备上的剩余电量，以及云端与设备之间的带宽。第三，基于优化问题的解决方案，我们的中间件将部分内容卸载到远程云端并返回相应的结果。在 MACS 之上的两个 Android 应用程序演示了我们方法的潜力。

我们 MACS 中间件的目标是实现弹性移动应用程序的执行。Zhang 等人 [20] 认为弹性应用具有两个不同的属性。首先，弹性执行部分在设备上、部分在云端进行。其次，这种划分不是静态的，而是在应用程序运行期间动态调整的。这种应用模型的用处在于，移动应用程序可以在移动平台上独立运行，但也可以根据需求和可用性访问云资源。因此，移动应用程序不再受到现有设备能力限制的约束。该方法的get细节在之前的工作 [38] 中有所介绍。

结果显示，通过卸载可以大幅减少本地执行时间（这有时对于用户来说等待是不可接受的），而通过将计算推送到远程云端，可以显著降低移动设备的 CPU 负载，这得益于远程云，因为大多数计算都被卸载到了远程云端。同时，可以节省大量的能量，这表明与本地执行相比，用户可以拥有更电池时间。结果还证明我们框架的开销很小。

## 3.5.5 总结

上述原型系统是以面向服务的架构开发的，这使得它们在多媒体和元数据层上实现了互操作性。这意味着某些服务的输出可以作为其他服务的输入。例如，用 AnViAnno 捕获、标记和注释的多媒体内容可以很容易地输入 MVCS 进行进一步的处理和语义增强。

表 3.4 总结了上述原型系统涵盖的云媒体服务。符号“X”表示相应的原型实现/使用了该服务。AnViAnno 和 SeViAnno 应用程序提供了对基本移动媒体操作的支持。通常，这些应用程序部署在云基础设施上，而移动和 Web 应用程序作为多媒体服务的前端。

## 76 云计算与数字媒体

表 3.4 用例原型总结、它们实现的云服务以及适用的移动云模型

| | 云多媒体服务 | | | | | | | | | | | | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | | | | | | 无处采集 | 实时通信 | 转码 | 索引与处理 | 协作 | 共享与标记 | 重定向 | 自适应流 | MAR | 自适应流 | 云端 | 云感知 | 雾云 |
| AnViAnno and SeViAnno | X | X | | | | | | | X | X | | X | X | X | |
| MVCS | X | X | X | | X | | | X | | X | | X | | | |
| MACS | | | | X | X | | X | | | | X | X |

MVCS 的重点是视频内容的重定向，以提高移动视频消费的用户体验（UX）。它使用不同的语义和计算机视觉策略来执行基于内容的视频流适配。此类操作可以在任何类型的移动云模型上执行，而本地执行消耗资源但始终可用，雾云模型提供了如卸载和低延迟等优势。XMMC 原型关注同事之间的实地协作。协作主要在多媒体元数据上进行。此外，XMMC 为通过 MAR 浏览器对生成的多媒体进行沉浸式消费提供了便利。相反，MACS 的目标增强移动设备的处理能力，根据需要适用于资源密集型媒体操作，如转码、处理、索引和重定向。这些示例原型提供了以多媒体格式表示知识的方法。这些应用程序的结合使用了之前描述的媒体理论操作。云计算的使用解决了动态 IS 工作负载和不断需求的问题。此外，高级服务（如语义重定向）改进了移动多媒体应用程序的用户体验。

## 3.6 结论与展望

本章旨在阐明移动云计算如何应用于支持专业社区的实践，特别是其需求，从多媒体和知识共享信息系统（ISS）的角度来看。专业社区表现出复杂的结构和动态过程，这反映在对信息的支持上。云资源的类实用型资源供给非常符合专业社区的成员性质。云计算的软件即服务（SaaS）概念为社区服务的无限制配置和混合提供了手段，以匹配任何新兴的 IS 要求。在本章中，我们识别了三种移动云计算模型，每种模型都有其优缺点，从媒体理论视角和组织理论视角可以考虑它们对多媒体服务 UX、可用性、响应性和成本的影响。这种视角的结合有助于我们理解专业社区内部的知识创造和学习过程。最后，本章要概述了我们小组开发的某些系统，这些系统涵盖了为专业社区 IS 支持所识别的大多数多媒体服务需求。实验结果为专业社区的移动云方法提供了支持。

## 参考文献

- 1. Klammara, R. and Jarke, M. 2008. Mobile social software for professional communities. UPGRADE, IX(3): 37–43.
- 2. Mell, P and Grance, T. 2009. NIST Definition of Cloud.
- 3. Armbrust, M., Fox, A., Griffiths, R., Joseph, A., Lee, G. 2009. Above the Clouds: A Berkeley View.
- 4. Wenger, E. and McDermott, R. 2002. Cultivating Communities.
- 5. Brown, J. S. and Duguid, P. 2000. Community of Practice.
- 6. Etienne, W. 1998. Social Life of Information.
- 7. Satnararayanan, M. 1996. Fundamental challenges in mobile computing.
- 8. Hassenzahl, M. and ISO 9241-210. 2010. Ergonomics of human system.
- 9. Hassenzahl, M. and Tractinsky, N. 2006. User experience—A research agenda.
- 10. Cui, Y., Chipchase, J., and Jung, Y. 2009. Personal TV: A survey.
- 11. Lagesse, B. J. 2011. Challenges in securing the interface between the cloud and mobile systems.
- 12. Barroso, L. A. and Holzle, U. 2009. The Datacenter as a Computer: Introduction to the Design of Warehouse-Scale Machines.
- 13. Satnararayanan, M. 2009. Case for VM-based computing.
- 14. Roel, K., Nicholas, P., Thilo, K., and Henri, B. 2010. Cuckoo: A computation offloading for smartphones.
- 15. Pearson, S. 2009. Taking account of privacy when designing cloud services.
- 16. Zhang, X., Kunithapatham, A., Jeong, S., and Gibbs, S. 2011. Towards an elastic application model for augmenting computing capabilities of mobile devices with cloud computing.
- 17. Zhang, X., Jeong, S., Kunithapatham, A., and Simon Gibbs. 2010. Towards an elastic application model for augmenting computing capabilities of mobile platforms.
- 18. Giurgia, I., Riva, O., Juric, D., Krivule, I., and Alonso, G. 2009. Calling the cloud: Enabling mobile phones as interfaces to cloud applications.

