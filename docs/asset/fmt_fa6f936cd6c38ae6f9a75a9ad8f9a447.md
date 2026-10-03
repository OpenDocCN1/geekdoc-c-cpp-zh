
# ROUTING AS CONSTRAINT SATISFACTION

- [Re96] Jean-Charles Rég, Generalized consistency for global constraints, Proceedings of the thirteenth international conference on artificial intelligence, Portland, Oregon, AAAI/ The MIT Press, 1996, pp. 209–215.
- [SFV95] Thomas Schiez, Hélène Fargier, and Gérard Verfaillie, Valued constraint satisfaction problems: Hard and easy problems, Chris Mellish (ed.), IJCAI-95: Proceedings, 14th International Conference on Artificial Intelligence, San Francisco, Manuel Kaufmann, 1995, pp. 631-637.
- [VLS96] Gérard Verfaillie, Michel Leaitre, and Thomas Schiez, solving constraint problems, Proceedings of the Thirteenth National Conference on Artificial Intelligence, Portland, Oregon, AAAI/ The MIT Press, 1996.
- [Wal96] Richard J. Wallace, Analysis of heuristic methods for partial constraint satisfaction, CP-96: Proceedings of the Second International Conference on Constraint Processing, Springer Verlag, 1996, pp. 482-496.
- [WF93] Richard J. Wallace and Eugene C. Freuder, Conjunctive heuristics for maximal constraint satisfaction, AAAI-93: Proceedings of 11th National Conference on Artificial Intelligence, Washington DC, AAAI/ The MIT Press, 1993, pp. 762-768.
- [YOH94] N. Yugami, H. Hara, Improving repair-based constraint satisfaction, 12th National Conference on Artificial Intelligence, Seattle, AAAI/ The MIT Press, 1994, pp. 344-349.
- [Yok97] Makoto Yokoo, Why adding constraints makes problem easier for hillclimbing algorithms: Analysing landscapes of CSPs, Smolka (ed.), CP-97: Proceedings of the Third International Conference on Principles and Practice of Constraint Processing, LNCS 1330, Springer Verlag, 1997, pp. 356-370.

# A Constraint-Based Approach to Satellite Scheduling

## ABSTRACT

Satellite scheduling, like all scheduling, is the problem of mapping tasks (observation, communication, downlink, control maneuvers, etc.) to resources (sensor satellites, relay satellites, ground stations, etc.). Through our work on satellite scheduling problems we have encountered many different constraints particular to the satellite domain. In this paper, we will introduce the satellite-operation scheduling problem, describing the constraints peculiar to satellite scheduling, and then present constraint-based modeling and heuristic methods that we have used to address these problems.

## 1. Introduction

In general, satellite scheduling is the problem of mapping tasks (observations, downlinks, control maneuvers, etc.) to resources (sensor satellites, relay satellites, ground stations, etc.). Satellite scheduling problems differ from traditional scheduling in several ways. Perhaps the most obvious difference between satellite scheduling and traditional scheduling is the fact that some of the resources (i.e., the satellites) are orbiting the Earth. This places an additional set of constraints on when a task can be executed, particularly because the satellite resources are only available to perform certain tasks in specific orbit. In addition, satellite scheduling problems require accurate modeling of task times, which can differ depending on the order in which tasks are performed.

Satellite-scheduling problems often involve periodic tasks, variable length tasks, and tasks that can be preempted. In addition, satellite-scheduling problems are usually constrained. Thus, satellite scheduling is usually viewed as a constraint-optimization problem (i.e. find the best possible set of tasks to schedule) rather than a constraint-satisfaction problem (i.e. find a solution that satisfies the constraints for all tasks).

Although the term satellite scheduling has been applied to many different aspects of a satellite's operation (e.g., design planning, launch control, lifecycle, etc.), we will focus on scheduling mission operations, namely the day-to-day activities of an operational satellite. Mission operation activities include payload (e.g., using a sensor on the satellite to collect data), bus operations (e.g., maintaining the health and status of the vehicle) and communications operations (e.g., transmitting data between satellites to the ground and receiving information or commands from a ground station).

Our work has addressed three general types of satellite missions: broadcast, telecommunications, and remote sensing, although a single satellite may encompass more than one. Broadcast satellites (e.g., DirectTV, PrimeStar, etc.) are typically geostationary (e.g., they remain fixed above a single point on the earth's surface), and are often used to broadcast to a large number of receivers. The satellites are geostationary to allow for fixed position ground-bound antenna. Telecommunication satellites (e.g., Telesdic, TDRS, etc.) relay information back and forth between ground stations (e.g., mobile phones, communications antenna). Historically, telecommunications have also been geostationary, but there has been a recent trend towards constellations of medium- or low-earth orbits (e.g., Iridium). Telecommunication scheduling problems are complicated by the fact that communications between a satellite and the ground can pass through relay satellites.

The mission of remote sensing satellites is to collect data and transmit the data to earth. With the exception of weather satellites (e.g., GOES), remote sensing satellites (e.g., Landsat, Hubble) typically reside in non-geationary orbits, and consequently the ground area visible to the satellite changes over time. Visibility windows affect the availability of satellites to perform tasks. In addition to visibility windows, other events can directly impact the availability of a resource. For example, a satellite ground station may be unavailable for maintenance. Any satellite scheduling system must consider these events when building a schedule.

When it is not possible to satisfy all requests for satellite operations, a priority system is typically used to choose which tasks to schedule. One possibility is for each task to assign a priority, and then a user defined objective function to compare the relative merit of partial schedules. In this case, satellite scheduling becomes a partial constraint satisfaction or constraint optimization problem [FW92].

This paper is organized as follows. Section 2 contains an overview of constraintbased scheduling, a satellite scheduling problem as an example. This allows us to introduce some satellite terminology. Section 3 describes satellite scheduling in detail including a discussion of periodic tasks, preemptive tasks, and priority-based optimization. Section 4 describes our general approach to satellite scheduling, including some discussion of our approach to satellite specific scheduling challenges. The last two sections discuss related work and future work.

## 2. Constraint-Based Satellite Scheduling

Satellite scheduling, like all scheduling, is the problem of mapping tasks (observation, communication, downlink, control maneuvers, etc.) to resources (sensor satellites, relay satellites, ground stations, etc.). We view this scheduling as a class of Constraint Satisfaction Problems (CSPs), or Constraint Optimization Problems when only a subset of the tasks can be assigned. A CSP is typically defined as a set of variables, a set of values for the variables, and a set of constraints on the values that can be assigned.

## 基于约束的卫星调度方法

……到变量。我们的基本方法可以描述为两个高层步骤：首先将卫星调度问题建模为一个约束满足问题（`CSP`），然后在给定的可用时间内找到最佳解决方案，其中“最佳”是相对于用户提供的目标函数定义的。我们要求所有方案（无论是部分的还是完整的）必须是可行的。我们使用“可行”一词是指满足所有所有任务和资源约束的调度计划。如果一个仅包含任务子集的部分调度计划满足所有已调度任务的约束，则该计划是可行的。

我们使用四种基本对象对调度问题建模：任务、资源、事件和约束。约束是需要执行的活动和操作。资源是完成任务所需的人员、卫星、传感器和通信通道。事件用于捕捉限制任务调度时间的特定领域情况（例如卫星可见窗口）。对于可调度的内容还有进一步的限制，这些限制由于与其他任务的相互作用，或者是由于资源容量和可用性引起的。

任务是通过分配一个满足所有相关约束的资源、开始时间和持续时间来调度的。如果一个任务需要多个资源（例如，下行任务需要卫星天线和地面站天线），则需要为其分配多个资源。更正式地说，一个已调度的任务是一个：

(`任务`, `资源集`, `开始时间`, `持续时间`)

当可以使用多个资源满足卫星资源需求时，调度器必须在这些替代资源之间进行选择。在任务没有资源选择的情况下，调度问题简化为为每个任务找到执行时间和持续时间。当任务具有固定持续时间时，调度问题进一步简化为为每个任务找到执行时间。
