If you develop enterprise applications, you have two opposing forces at work. On one side is your marketing department. It wants as many simultaneous users on the application as possible. This drives its commerce model and makes money. On the other side is the hardware implementation team, who tells you there’s a limit to the number of users that the hardware will support. What is a developer to do?

There’s more to the problem than just limited bandwidth. What happens when the application server goes down? All your customers are out of luck, and you can hear the marketing staff down the hall when they realize that all their carefully crafted plans are out the window until the server is back up.

As you’ve probably guessed by the title of this chapter, is to implement COM+ load balancing. It’s a solution that’s easy to implement and requires no change in your programming model for almost all cases.

Before you get too far into this chapter, I need to warn you that as of the writing of this book, component load balancing is not part of COM+. I cover the reasons for this at the end of the chapter and talk about its future.

# # Component Load Balancing Defined

*Load balancing*, simply put, is the distribution of work among several computers. Many times these computers are referred to as *cluster machines*. There is always one central point that distributes the work among the cluster machines. This is known as the *load-balancing server*, or the router. The router can also act as one of the cluster machines. Conceivably a machine could be managing and assigning requests as a router, while satisfying some of the requests as a cluster machine.

The *term unit of work* is used when discussing load balancing. The unit of work is a chunk of work performed by a cluster machine. Usually the designers of a technology determine the unit of work. In this case the engineers from Microsoft have done just that. I discuss the unit of work at greater length in the section “Parallelism and Granularity.”

*Granularity*, as referenced in this chapter, is the size of the work chunks that are distributed. The greater the chunk of work doled out to a cluster machine, the coarser is its granularity. The smaller the chunk of work doled out to a cluster machine, the finer is its granularity.