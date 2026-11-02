
技术，例如关联规则挖掘、决策树、回归、支持向量机以及其他数据挖掘技术[37]。

然而，这些解决方案中很少有从大数据的存储和处理角度，完整解决将HPC与当前新兴技术相集成的问题，尤其是那些从社交媒体中提取的数据。目前用于托管和处理大数据的一些最流行技术是云计算、HDFS和Hadoop MapReduce[38]。目前，HPC在云计算中的使用仍然有限。美国能源部国家实验室（DOE）迈出了这项研究的第一步，开始探索将云服务用于科学计算[24]。此外，2009年，Yahoo Inc.与美国主要顶尖大学建立合作关系，以开展更多关于云计算、分布式系统和高性能计算应用的研究。

最近，已有若干研究评估了云中高性能计算的性能。这些研究大多使用亚马逊弹性计算云（Amazon EC2）作为云环境[26,39–42]。此外，只有少数研究评估了将新兴分布式范式与云环境相结合时高性能计算的性能[43]。例如，在文献39中，作者在三个不同的云提供商上评估了HPC：Amazon EC2、GoGrid云和IBM云。对于每个云平台，他们在Linux虚拟机（VM）上运行HPC，并得出结论：所测试的公共云似乎并未针对运行HPC应用进行优化。其原因在于公共云平台中VM之间的网络连接较慢。此外，文献26的作者评估了HPC应用在当前云环境（Amazon EC2）中的性能，以理解迁移到云时的权衡。总体结果表明，在EC2云平台上运行HPC会限制性能并导致显著波动。除Amazon EC2外，研究[44]还评估了在三个不同平台上运行HPC应用的性能-成本权衡。第一个和第二个平台由两个物理集群（Taub和Open Cirrus集群）组成，第三个平台由采用基于内核的虚拟机（KVM）虚拟化的Eucalyptus组成。在这些平台上运行HPC使作者得出结论：对于低通信密集型应用，云更具成本效益。

也有研究使用不同虚拟化技术对HPC进行评估，而未将其与新的云技术相关联[45–48]。例如，在文献45中，作者分析了包括VMware、Xen和OpenVZ在内的虚拟化技术。他们的发现表明，没有一种技术能完全匹配基础系统的性能；然而，OpenVZ在文件系统性能和行业标准基准方面均表现出高性能。在文献46中，作者比较了KVM和VMware的性能。总体发现表明，VMware的性能优于KVM。不过，在少数情况下，KVM给出的结果优于VMware。在文献47中，作者对两个领先的开源虚拟机管理程序Xen和KVM进行了定量分析。他们的研究评估了每种虚拟化技术下VM的性能隔离、整体性能和可扩展性。简而言之，他们的发现表明，KVM在客户机崩溃方面存在重大问题（当增加客户机数量时）；然而，KVM的性能隔离仍优于Xen。最后，在文献48中，作者广泛比较了四种虚拟机管理程序：Hyper-V、KVM、VMware和Xen。他们的结果表明，没有完美的虚拟机管理程序。然而，尽管评估了不同技术，HPCaaS仍需更多研究，以确定适合大数据分析的环境。

在我们最近的工作中，已在三个不同集群上进行了不同实验：Hadoop物理集群（HPhC）、使用KVM的Hadoop虚拟化集群（HVC-KVM）和使用VMware Elastic Sky X Integrated的Hadoop虚拟化集群（HVC-VMware ESXi），如图5.1所示[49]。

使用两个主要基准——TeraSort和HDFS I/O饱和（TestDFSIO）基准[50]——来研究机器虚拟化对HPCaaS的影响。TeraSort会执行大量计算、网络和存储输入/输出（I/O），通常被认为能代表真实的Hadoop工作负载。TestDFSIO基准用于通过写和读操作检查Hadoop集群的I/O速率。此类基准有助于通过检查网络性能以及测试硬件、操作系统和Hadoop设置来测试HDFS。例如，图5.2显示了在HPHC上运行TeraSort基准和TestDFSIO-Write时获得的一些实验结果。

![](img/1643181e79c76dc765d55a7355afb4a4_137_0.png)

图5.2 在Hadoop物理集群上的性能：(a) TeraSort和(b) TestDFSIO-Write。（引自 Achahbar, O.，《虚拟化对云中高性能计算集群的影响》，硕士学位论文报告，摩洛哥伊夫兰Al Akhawayn大学，2014年。）

图5.2a表明，对10 GB和30 GB等大型数据集进行排序需要大量时间。然而，将集群扩展到更多节点显著减少了数据集排序所需的时间。图5.2b表明，随着VM数量增加，写入不同大小数据集时的平均时间减少。事实上，Hadoop VMware ESXi集群在对大数据集排序（计算更多）方面表现更好，而Hadoop KVM集群在I/O操作方面表现更好。

此外，尽管已经开发出若干并行机器学习算法，并使用传统HPC架构将其集成到云环境中，但其他技术在新兴技术（如图形处理单元（GPU）[51]）中仍未得到充分利用。值得注意的是，基于GPU的计算是并行计算中的巨大范式转变，有望带来性能的显著提升。GPU是为计算密集型应用而设计的；它们允许在更多处理单元上执行线程。拥有大量线程使得超越当前多核CPU的性能成为可能。

如今，GPU编程环境比几年前丰富得多。在两种主要编程语言——统一计算设备架构（CUDA）[52]和开放计算语言（OpenCL）——之上，已经开发出一些库，使人们无需详细了解或编程GPU硬件即可快速访问GPU的计算能力。GPU[53]可用作大数据分析的加速器，例如用于社交媒体、传感器数据流中的统计分析、预测模型等。GPU还可集成到云计算中，为大数据提供GPU加速的云服务。例如，由于GPU并不昂贵且性能优于多核机器，它们可以作为云环境的实用基础设施。此外，大部分工作一直致力于机器学习

- 15. MongoDB。可从 http://www.mongodb.org/ 获取。
- 16. Apache CouchDB™。可从 http://couchdb.apache.org/ 获取。
- 17. D. Boulter，《简化你的云之旅》，Capgemini and SOGETI，2010，第1–8页。
- 18. P. Mell 和 T. Grance，《NIST云计算定义》，美国国家标准与技术研究院，2011，第1–3页。
- 19. A. E. Youssef，《探索云计算服务与应用》，《新兴计算与信息科学趋势杂志》，第3卷，第6期，第838–847页，2012年。
- 20. A. T. Velte、T. J. Velte 和 R. Elsenpeter，《云计算：实用方法》，第1版，McGraw-Hill Osborne Media，纽约，352页，2009年。
- 21. Amazon Web Services。可从 http://aws.amazon.com/ 获取。
- 22. Google Cloud Platform。可从 https://cloud.google.com/ 获取。
- 23. J. Bernstein 和 K. McMahon，《按需计算——HPC即服务》，第1–12页，Penguin On Demand。可从 http://www.penguincomputing.com/files/whitepapers/PODWhitePaper.pdf 获取。
- 24. Y. Xiaotao、L. Aili 和 Z. Lin，《云环境中的高性能计算研究》，载于第三届计算机科学与计算技术国际研讨会（ISCSCT），2010，第289–293页。
- 25. 自助POD门户。可从 http://www.penguincomputing.com/services/hpc-cloud/pod 获取。
- 26. K. R. Jackson，《Amazon Web Services云上高性能计算应用的性能分析》，载于《云计算技术与科学（CloudCom）》，2010年IEEE第二届国际会议，2010，第159–168页。
- 27. Amazon Cloud Storage。可从 http://aws.amazon.com/ec2/reserved-instances/ 获取。
- 28. Amazon Cloud Drive。可从 http://aws.amazon.com/ec2/spot-instances/ 获取。
- 29. 面向开发人员的Microsoft高性能计算。可从 http://msdn.microsoft.com/en-us/library/f976568.aspx 获取。
- 30. Google Cloud Storage。可从 https://cloud.google.com/products/compute-engine 获取。
- 31. D. Pop，《机器学习与云计算：分布式和SaaS解决方案综述》，蒂米什瓦拉e-Austria研究所技术报告，2012年。
- 32. A. Ghoting、P. Kambadur、E. Pednault 和 R. Kannan，《NIMBLE：在MapReduce上实现并行数据挖掘和机器学习算法的工具包》，载于KDD，2011年。
- 33. J. Dean 和 S. Ghemawat，《MapReduce：大型集群上的简单数据处理》，载于OSDI，2004，第1–12页。
- 34. Hadoop。可从 http://hadoop.apache.org/ 获取。
- 35. S. Krishnan、M. Tatineni 和 C. Baru，《MyHadoop——传统HPC资源上的按需Hadoop》，载于美国国家科学基金会集群探索计划，2011，第1–7页。
- 36. E. Molina-Estolano、M. Gokhale、C. Maltzahn、J. May、J. Bent 和 S. Brandt，《在并行文件系统上混合Hadoop和HPC工作负载》，载于第四届千万亿级数据存储年度研讨会，2009，第1–5页。
- 37. S. R. Upadhyaya，《机器学习的并行方法——全面综述》，《并行与分布式计算杂志》，第73卷，第284–292页，2013年。
- 38. C. Cranor、M. Polte 和 G. Gibson，《使用PLFS在Hadoop存储上进行HPC计算》，卡内基梅隆大学并行数据实验室，2012，第1–9页。
- 39. S. Zhou、B. Kobler、D. Duffy 和 T. McGlynn，《在公共云中运行HPC应用的案例研究》，载于Science Cloud ’10，2012年。
- 40. E. Walker，《面向高性能科学计算的Amazon EC2基准测试》，德克萨斯大学德克萨斯高级计算中心，2008，第18–23页。
- 41. J. Ekanayake 和 G. Fox，《利用云和云技术的高性能并行计算》，印第安纳大学信息学与计算学院，2009，第1–20页。
