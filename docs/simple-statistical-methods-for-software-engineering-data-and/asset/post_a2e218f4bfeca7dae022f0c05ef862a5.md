
![](img/2f042205c6c0e14747f198ed8f9c9f40_117_0.png)

## Figure 6.3 Tracking project progress.

In EVM terminology, this is referred to as *budgeted cost of work*. From a project plan, one can see how the project value increases with time. The project is said to “earn value” as work is completed. To measure progress, we define the following metrics.

Planned value = budgeted cost of work scheduled (BCWS)
Earned value = budgeted cost of work performed (BCWP)

An example of project progress tracked with these two metrics is shown in Figure 6.3.

At a glance, one can see how earned value trails behind planned value, graphically illustrating project progress. This is known as the *earned value graph*.

## Tracking Project Cost

The actual cost expended to complete the work reported is measured as the actual cost of work performed (ACWP). Cost information can be included in the earned value graph, as shown in Figure 6.4.

In addition to the earned value graph, we can compute performance indicators such as project variances and performance indices. We can also predict the time and cost required to finish the project using linear extrapolation. These metrics are listed in Data 6.1.

An earned value report would typically include all the earned value metrics and present graphical and tabular views of project progress and project future.

![](img/2f042205c6c0e14747f198ed8f9c9f40_118_0.png)

## Figure 6.4 Tracking project cost.

## Data 6.1 Earned Value Metrics

Core Metrics

- Budgeted cost of work scheduled (BCWS) (also planned value [PV])
- Budgeted cost of work performed (BCWP) (also earned value [EV])
- Actual cost of work performed (ACWP) (also actual cost [AC])

Performance Metrics

- Cost variance = PV – AC
- Schedule variance = EV – PV
- Cost performance index (CPI) = EV/AC
- Schedule performance index (SPI) = EV/PV
- Project performance index (PPI) = SPI × CPI
- To complete schedule performance index (TCSPI)

Predictive Metrics

- Budget at completion = BAC
- Estimate to complete (ETC) = BAC – EV
- Estimate at completion (EAC)
  - EAC = AC + (BAC – EV) Optimistic
  - EAC = AC + (BAC – EV)/CPI Most likely
  - EAC = BAC/CPI Most likely*simple (widely used)
  - EAC = BAC/PPI Pessimistic
- Cost variance at completion (VAC) = BAC – EAC

The project management body of knowledge (PMBOK) treats earned value metrics as crucial information for the project manager. Several standards and guidelines are available to describe how EVM works. For example, the EVMS standard released by Department of Energy (DOE) utilizes the EVMS information as an effective project management system to ensure successful project execution.

## BOX 6.4 WHY IS SIZE METRIC MISSING?

We measure the size of what we build. If we construct a house, we measure the floor area. If we build a truck, we measure its length, height, and breadth, among other parameters. Size measurement is a hallmark of engineering.

When we build a software, we are reluctant to measure size. Some of us do not measure size at all. This is a disappointment for we have failed to uphold software engineering. Come to think of it, it is rather easy to measure size. If we find IFPUG function point or FFP time consuming and cumbersome, especially for large modules, we have alternatives to choose from. For example, we can use any of the following established metrics:

- Albrecht function point
- Mark II FP
- Object point
- Test case point
- Use case point
- PROBE
- Feature point

Doug Hubbard’s book titled *How to Measure Anything* [10] can help to overcome mental barriers in measuring things considered impossible to measure. He observes that the perceived impossibility of measurement is an illusion caused by not understanding the concept of measurement, the object of measurement, and the methods of measurement.

You can build your own proprietary size metric. Some have constructed engineering size unit as a metric. Others have invented requirement size unit. Homegrown complexity metrics are doing the rounds as well. Having an approximate size metric is infinitely better than not having one.

## Review Questions

- 1. Mention your choice of a product metric in software development.
- 2. Mention your choice of a process metric in software development.
- 3. Mention your choice of a project metric in software development.
- 4. Mention your choice of a process for establishing subprocess metrics. Identify and list the subprocess metrics for the process you have selected.
- 5. Why is function point a success?

## Suggested Readings

Aczel, A. D. and J. Sundara Pandian, *Complete Business Statistics*, McGraw-Hill, London, 2008.

*Applying Earned Value Analysis to Your Project.* Available at http://office.microsoft.com/en-in/project-help/applying-earned-value-analysis-to-your-project-HA001021179.aspx.

Astels, D. *Test-Driven Development: A Practical Guide*, Prentice Hall PTR, Upper Saddle River, NJ, 2003.

Cem, K. *Rethinking Software Metrics*, STQE, March/April 2000.

*Estimated Function Point.* Available at http://www.functionpoints.org/, http://www.functionpoints.org/resources.html, http://csse.usc.edu/csse/event/1998/COCOMO/18_Stensrud%20Estimating.pdf.

*Function Point Estimation.* Available at http://webcourse.cs.technion.ac.il/234270/Spring2013/ho/WCFiles/function%20points%20estimation.pdf.

Garmus, D. *An Introduction to Function Point Counting.* Available at http://www.compaid.com/caiinternet/ezine/garmus-functionpointintro.pdf.

Hunt, R. P., P. J. Solomon and D. Galorath, *Applying Earned Value Management to Software Intensive Programs.* Available at http://www.galorath.com/DirectContent/applying_earned_value_management_to_software_intensive_programs.pdf.

International Function Point Users Group, *IT Measurement: Practical Advice from the Experts*, Addison-Wesley, 2002.

Kitchenham, B. *Software Metrics—Measurement for Software Process Improvement*, NCC Blackwell, UK, 1996.

Kulik, P. *Software Metrics: State of the Art—2000*, KLCI, 2000.

Kusters, R., A. Cowderoy, F. Heemstra and E. van Veenendaal, editors, *Project Control for Software Quality*, Shaker Publishing, 1999.

McBreen, P. *Software Craftsmanship: The New Imperative*, Addison-Wesley Professional, 2002.

McCarthy, J. *Dynamics of Software Development*, Microsoft Press, 1995.

McConnell, S. *Professional Software Development*, Addison-Wesley, 2004.

Meli, R. and L. Santillo, *Function Point Estimation Methods: A Comparative Overview.* Available at http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.33.6479&rep=rep1&type=pdf.

Norman, F. E., and M. Neil, *Software Metrics: Road Map*, CSD QM&WC, London, August 2000.

Parthasarathy, M. A. *Practical Software Estimation*, Addison-Wesley, 2007.

Platt, D. S. *Why Software Sucks—And What You Can Do about It*, Addison-Wesley Professional, 2007.

Putnam, L. H. and W. Myers, *Expert Metrics Views*, Cutter Information Group, 2000.

Wiegers, K. E. *Practical Project Initiation: A Handbook with Tools*, Microsoft Press, 2007.

Woodings, T. L. *A Taxonomy of Software Metrics*, Software Process Improvement Network (SPIN), Perth, 1995.

## Chapter 7

## Maintenance Metrics

## Fusion of Frameworks in Software Maintenance

Software maintenance assimilates three management styles: project management, operations management, and service management. Maintenance metrics design mirrors this fusion. The big maintenance work gains from project management framework, the small tasks gain from operations management, and all maintenance tasks, by necessity, subscribe to service management framework. The project approach harmonizes all.

> Operations keeps the lights on, strategy provides a light at the end of the tunnel, but project management is the train engine that moves the organization forward.
> 
> Joy Gumz

Maintenance engineering is based on multiple principles. On the one side, we have enhancement tasks (adaptive maintenance), which are mini projects to change the functionality of software [1]. Knowledge areas from Project Management Body of Knowledge (PMBOK) are often used as founding principles. On the other side, we have quick jobs of bug fixing (corrective maintenance), which are more like service tasks. Managing these tasks uses operations management, ITIL, ISO 20000, and CMMi SM concepts as founding principles. Metrics in these two different types of maintenance accordingly differ in their scope, nature, and intent. Metrics interpretations reflect the respective founding principles.
