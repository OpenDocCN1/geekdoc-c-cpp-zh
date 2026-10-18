# POWER ANALYSIS FOR APPLICATIONS AND DATA CENTERS

Taylor Kidd*, Rob Farber†, Belinda Liviero*, Evan Felix‡
Intel Corporation, USA* TechEnablement Corporation, USA†
Pacific Northwest National Laboratory, USA‡

# INTRODUCTION TO MEASURING AND SAVING POWER

In this chapter, we look at two pearls that can potentially save megawatts of power on leadership class systems and provide significant reductions in power consumption on small clusters over the long term. These pearls are: (1) how to measure the performance per watt associated with running an application, analyze such measurements, and make changes to an application to improve its energy efficiency; and (2) how to acquire and understand power usage across a cluster environment through the use of waterfall plots.

With this in mind, we wrote this chapter in three sections: Sections “Introduction to measuring and saving power,” “Application: Power measurement and analysis,” and “Data center: Interpretation via waterfall power data charts.” This section includes some power management and threading background, and provides an overall context for the subsequent sections. Section “Application: Power measurement and analysis” discusses the basics of how to measure and analyze performance per watt for a specific application. Section “Data center: Interpretation via waterfall power data charts” looks at techniques you can use to analyze data center power-performance.

# MOTIVATION TO ACT: IMPORTANCE OF POWER OPTIMIZATION

Large data center installations have been experiencing a focus shift in operating metrics from maximum performance alone to performance per watt. Most of today’s (and future) procurements specify system requirements that include the operational maximum and average power consumption envelope while the system is running the target applications it has been designed for. Therefore, performance per watt is a key driver of system design, and, more recently, of application development. “Performance at any cost” is no longer viable as supercomputer cluster operational costs are now on par with the hardware and software acquisition cost. It has been estimated that an exascale machine, built with technology available in 2014, would consume several gigawatts of power (versus contemporary petascale systems that consume 5-20 mW). New technology needs to be developed to make exascale computing practical. Furthermore, the environmental impact of large systems is substantial, causing data center location considerations to include less expensive and/or more environmentally friendly sources such as