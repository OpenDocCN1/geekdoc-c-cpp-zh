# Lambdas!?

The Lambda Architecture appeared in the excellent [“Big Data: Principles and best practices of scalable realtime data systems”](http://www.amazon.co.uk/Big-Data-Principles-practices-scalable/dp/1617290343) by Nathan Marz and James Warren. It’s main aim is to provide an architecture to support both streams and batch data processing applications, but that’s not where its impact necessarily needs to stop!

![](bbox=[0.2693, 0.3567, 0.7289, 0.5393])

Two main areas are identified, a Batch or Slow-data area with pre-computed views that are then used to produce a Servicing Layer with actual views for querying, and a Speed or Fast-Data area that provides direct flows to Views.

When we overlay this architecture with the patterns in this chapter, we can start to see that there’s a lot of commonality between the two.

26. http://www.amazon.co.uk/Big-Data-Principles-practices-scalable/dp/1617290343