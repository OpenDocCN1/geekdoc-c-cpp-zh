
the scheduler’s power. The genetic scheduler has an estimation phase, where the processing data speed for each application is measured. The scheduler ensures that, once an application’s execution has started, that application will end successfully in normal conditions. The Hadoop On Demand (HOD) [3] virtual cluster uses the Torque resource manager for node allocation and automatically prepares configuration files. Then it initializes the system based on the nodes within the virtual cluster. HOD can be used in a relatively independent way.

To support multiuser situations [14,17], the Hadoop framework incorporates several components that are suitable for Big Data processing (Figure 6.3) since they offer high scalability through a large volume of data and support access to widely distributed data. Here is a very short description of these components: Hadoop Common consists of common utilities that support any Hadoop modules and any new extension. HDFS provides high-throughput access to application data. Hadoop YARN (Apache Hadoop NextGen MapReduce) is a framework for job scheduling and cluster resource management that can be extended across multiple platforms. Hadoop MapReduce is a YARN-based system for parallel processing of large data sets.

Facebook solution Corona [18] extends and improves the Hadoop model, offering better scalability and cluster utilization, lower latency for small jobs, the ability to upgrade without disruption, and scheduling based on actual task resource requirements rather than a count of map and reduce tasks. Corona was designed to answer the most important Facebook challenges: unique scalability (the largest cluster has more than 100 PB of data) and processing needs (crunch more than 60,000 Hive queries a day). The data warehouse inside Facebook has grown by 2500 times between 2008 and 2012, and it is expected to grow by the same factor until 2016.

![](img/1643181e79c76dc765d55a7355afb4a4_148_0.png)

FIGURE 6.3 Hadoop processing and Big Data platforms.

![](img/1643181e79c76dc765d55a7355afb4a4_151_0.png)

FIGURE 6.5 Resource allocation process.

A general-purpose resource management approach in a cluster used for Big Data processing should make some assumptions about policies that are incorporated in service-level agreements. For example, interactive tasks, distributed and parallel applications, as well as noninteractive batch tasks should all be supported with high performance. This property is a straightforward one but, to some extent, difficult to achieve. Because tasks have different attributes, their requirements to the scheduler may contradict in a shared environment. For example, a real-time task requiring short-time response prefers space-sharing scheduling; a noninteractive batch task requiring high throughput may prefer time-sharing scheduling [6,29]. To be general purpose, a trade-off may have to be made. The scheduling method focuses on parallel tasks, while providing an acceptable performance to other kinds of tasks.

YARN has a pluggable solution for dynamic policy loading, considering two steps for the resource allocation process (Figure 6.5). Resource allocation is done by YARN, and task scheduling is done by the application, which permits the YARN platform to be a generic one while still allowing flexibility of scheduling strategies. The specific policies in YARN are oriented on resource splitting according to schedules provided by applications. In this way, the YARN's scheduler determines how much and in which cluster to allocate resources based on their availability and on the configured sharing policy.

### 6.6 OPTIMIZATION TECHNIQUES FOR SCHEDULING

The scheduling in Big Data platforms is the main building block for making data centers more available to applications and user communities. An example of optimization is multiobjective and multiconstrained scheduling of many tasks in Hadoop [30] or optimizing short jobs with Hadoop [31]. The optimization strategies for scheduling are specific to each model and for each type of application. The most used techniques for scheduling optimization are as follows:

- Linear programming allows the scheduler to find the suitable resources or cluster of resources, based on defined constraints.
- *Dynamic partitioning* splits complex applications in a cluster of tasks and schedules each cluster with a specific scheduling algorithm.
- *Combinatorial optimization* aims to find an optimal allocation solution for a finite set of resources. This is a time-consuming technique, and it is not recommended for real-time processing.
- *Evolutionary optimization* aims to find an optimal configuration for a specific system within specific constraints and consists of specific bioinspired techniques like genetic and immune algorithms, ant and bee computing, particle swarm optimization, and so forth. These methods usually find a near-optimal solution for the scheduling problem.
- *Stochastic optimization* uses random variables that appear in the formulation of the optimization problem itself and are used especially for applications that have a deterministic behavior, that is, a normal distribution (for periodic tasks) or Poisson distribution (for sporadic tasks), and so forth.
- *Task-oriented optimization* considers the task’s properties, arrival time (slack optimization), and frequency (for periodic tasks).
- *Resource-oriented optimization* considers completion time constraints while making the decision to maximize resource utilization.

### 6.7 CASE STUDY ON HADOOP AND BIG DATA APPLICATIONS

We can consider that, on top of Apache Hadoop or a Hadoop distribution, you can use a Big Data suite and scheduling application that generate Big Data. The Hadoop framework is suitable for specific high-value and high-volume workloads [32]. With optimized resource and data management by putting the right Big Data workloads in the right systems, a solution is offered by the integration of YARN with specific schedulers: G-Hadoop [33], MPI Scheduler, Torque, and so forth. The cost-effectiveness, scalability, and streamlined architectures of Hadoop have been developed by IBM, Oracle, and Hortonworks Data Platform (HDP) with the main scope to construct a Hadoop operating system. Hadoop can be used in public/private clouds through related projects integrated in the Hadoop framework, trying to offer the best answer to the following question: What type of data/tasks should move to a public cloud, in order to achieve a cost-aware cloud scheduler [34]?

Different platforms that use and integrate Hadoop in application development and implementation consider different aspects. Modeling is the first one. Even in Apache Hadoop, which offers the infrastructure for Hadoop clusters, it is still very complicated to build a specific MapReduce application by writing complex code. Pig Latin and Hive query language (HQL), which generate MapReduce code, are optimized languages for application development. The integration of different scheduling algorithms and policies is also supported. The application can be modeled in a graphical way, and all required code is generated. Then, the tooling of Big Data services within a dedicated development environment (Eclipse) uses various dedicated plugins. Code generation of all the code is automatically

### 6.8 CONCLUSIONS

In the past years, scheduling models and tools have been faced with fundamental re-architecting to fit as well as possible with large many-task computing environments. The way that existing solutions were redesigned consisted of splitting the tools into multiple components and adapting each component according to its new role and place. Workloads and workflow sequences are scheduled at the application side, and then, a resource manager allocates a pool of resources for the execution phase. So, the scheduling became important at the same time for users and providers, being the most important key for any optimal processing in Big Data science.

## REFERENCES

- 1. M. D. Assuncao, R. N. Calheiros, S. Bianchi, M. A. Netto, and R. Buyya. Big Data computing and clouds: Challenges, solutions, and future directions. arXiv preprint arXiv:1312.4722, 2013. Available at http://arxiv.org/pdf/1312.4722v2.pdf.
- 2. A. Rasooli, and D. G. Down. COSHH: A classification and optimization based scheduler for heterogeneous Hadoop systems. Future Generation Computer Systems, vol. 36, pp. 1–15, 2014.
- 3. M. Tim Jones. Scheduling in Hadoop. An introduction to the pluggable scheduler framework. IBM developerWorks, Technical Report, December 2011. Available at https://www.ibm.com/developerworks/opensource/library/os-hadoop-scheduling.
- 4. L. Zhang, C. Wu, Z. Li, C. Guo, M. Chen, and F. C. M. Lau. Moving Big Data to the cloud: An online cost-minimizing approach. Selected Areas in Communications, IEEE Journal on, vol. 31, no. 12, pp. 2710–2721, 2013.
- 5. Cisco Report. Big Data Solutions on Cisco UCS Common Platform Architecture (CPA). Available at http://www.cisco.com/c/en/us/solutions/data-center-virtualization/big-data/index.html, May 2014.
- 6. V. Cristea, C. Dobre, C. Stratan, F. Pop, and A. Costan. Large-Scale Distributed Computing and Applications: Models and Trends. IGI Global, Hershey, PA, pp. 1–276, 2010. doi:10.4018/978-1-61520-703-9.
- 7. D. Pletea, F. Pop, and V. Cristea. Speculative genetic scheduling method for Hadoop environments. In 2012 14th International Symposium on Symbolic and Numeric Algorithms for Scientific Computing, SYNASC, pp. 281–286, 2012.
- 8. A.-M. Oprescu, T. Kielmann, and H. Leahu. Budget estimation and control for bag-of-tasks scheduling in clouds. Parallel Processing Letters, vol. 21, no. 2, pp. 219–243, 2011.
- 9. M. Mao, J. Li, and M. Humphrey. Cloud auto-scaling with deadline and budget constraints. In The 11th ACM/IEEE International Conference on Grid Computing (Grid 2010). Brussels, Belgium, 2010.
- 10. J. Yu, and R. Buyya. Scheduling scientific workflow applications with deadline and budget constraints using genetic algorithms. Scientific Programming Journal, vol. 14, nos. 3–4, pp. 217–230, 2006.
- 11. K. Liu, H. Jin, J. Chen, X. Liu, D. Yuan, and Y. Yang. A compromised-time-cost scheduling algorithm in swindew-c for instance-intensive cost-constrained workflows on a cloud computing platform. International Journal of High Performance Computing Applications, vol. 24, no. 4, pp. 445–456, 2010.
- 12. T. White. Hadoop: The Definitive Guide. O’Reilly Media, Inc., Yahoo Press, Sebastopol, CA, 2012.
- 13. X. Hua, H. Wu, Z. Li, and S. Ren. Enhancing throughput of the Hadoop Distributed File System for interaction-intensive tasks. Journal of Parallel and Distributed Computing, vol. 74, no. 8, pp. 2770–2779, 2014. ISSN 0743-7315.
