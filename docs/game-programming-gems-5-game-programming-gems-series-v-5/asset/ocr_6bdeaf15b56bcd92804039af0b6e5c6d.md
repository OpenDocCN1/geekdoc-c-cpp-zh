+   1. Define the information to load/unload.
+   2. Define the size of each block of information.
+   3. Divide the search space into blocks.
+   4. Define the necessary structures to manage all the blocks.
+   5. Every time it is needed, check the information to load/unload, walking along all the blocks of the search space.

As you may have noticed, this solution is highly inefficient. It spends too much time in the division of the search space and consumes many resources, which is necessary in maintaining such complex structures with so much information for each block. Checking everything is excessively costly, too, and this solution is limited to loading/unloading the type of information defined by the design. If another type of information is required, it may be necessary to redesign the entire paging system! Finally, all these problems increase exponentially as soon as the search space grows, so let's go ahead and take the time to do it well the first time around.

# The GP Paging Solution: Only Check What You Need

GP solves all the aforementioned problems in a really easy way through simple and intuitive interfaces. The main features of GP include the following:

+   Almost complete transparency for the designer and user
+   Search-space size independence
+   No preprocessing, space divisions, or complex structures
+   Memory only contains indispensable data
+   Multiuser transparency (for the designer and the user)
+   Information agnostic

The following sections will progressively describe the design of GP and some details of the implementation. It is worth noting that this implementation is not unique; GP can be implemented as desired, using most high-level programming languages and paradigms.

# The Index Is the Key

In GP, as well as in other traditional paging systems, it is necessary to define the size of each block of information that will be loaded/unloaded. We will also define a mechanism to locate each block in the search space, along with a unique identifier per block.

We begin with a class called spindex that manages this information, thereby fulfilling three functions simultaneously:

+   Define the size of the paging block.
+   Locate the block in the search space.
+   Uniquely identify the block.