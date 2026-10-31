# Common Design Challenges

# Objectives

Complex-event processing solutions often present some significant design challenges. This chapter covers the challenges you are most likely to encounter in your designs. After reading this chapter you will be able to

+   - Describe how information can be shared
+   - Describe how locking can be used to maintain data integrity
+   - Describe the approaches for managing sequencing constraints
+   - Describe the approaches for managing event duplication

# Information Sharing

As soon as a solution is modularized and those modules are deployed in different agents, the problem of sharing information between the modules arises. There are two main approaches for information sharing. One is to use an event to convey the information directly from one module to another. The other is to use the cache as an intermediary.