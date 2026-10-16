Managing threads in this way can be difficult and error prone. The most complicated aspect of managing threads manually is the fact that the ideal number of threads for your application varies depending on how many other system threads are currently running as well as how many cores exist on the machine you’re running on. In an ideal world, you want to spawn just the right amount of threads to take advantage of 100 percent of your CPU resources. Knowing how many threads would achieve this goal is difficult for you, the programmer. Recently, Apple added some new threading capabilities to Objective-C to address exactly this conundrum. The centerpiece of this new threading model is called Grand Central Dispatch.

Grand Central Dispatch is centered around the classes NSOperation and NSOperationQueue. These two classes together provide a high-level object-oriented abstraction for dealing with threads as individual atomic tasks.

The core class of this suite of classes is NSOperation. The NSOperation class provides a base class for you to inherit from for the purposes of defining a task to be executed on a background thread. You can think of an NSOperation object as an instance of a task that you want to perform. You inherit from the NSOperation class and create your own custom operation class. You then instantiate this custom operation class and hand the operation off to an NSOperationQueue which is responsible for managing the operation. NSOperationQueue will even spawn whatever necessary threads are appropriate for having that task operate in the background. The NSOperationQueue, under the covers, leverages Grand Central Dispatch and launches an appropriate number of background threads to handle however many operations you feed to it. Operations can be configured with dependencies such that a given operation will not be started until all of its dependencies have already been completed. Additionally, the queues can be configured to run in parallel or to execute their operations serially.

# CROSS-REFERENCE

Chapter 5 also discusses some of the low level Objective-C functions you can use for interacting with Grand Central Dispatch.

# NOTE

Some developers who are new to Objective-C mistakenly think that NSOperationQueue is a useful tool for simply serializing tasks one after another on the current thread. This is incorrect. NSOperationQueue is really better used in association with background threads. This is its default operation.

# Creating operations

NSOperation and NSOperationQueue are ideally suited to tasks that are “embarrassingly parallel.” These are tasks which have no real dependencies, but which consist of CPU bound