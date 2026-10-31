If the application design is done in such a way that different parts can be distributed independently, we recommend putting the parts of the application in different SCs, because the smallest distribution granularity in software logistics is the software component. The SC is also the entity that is versioned, so the SC is the entity that is meant to structure the deployment.

There are other reasons to define SCs, such as project organization and semantic reasons.

# Development Component Granularity

The different domains provide separate DC types. It is therefore a good choice (and sometimes the only option) to put the content for different domains in separate DCs. Therefore, all process content is located in a process composer DC, all Web Dynpro content is part of a Web Dynpro DC, and so on.

A DC is the atom of reuse, that is, the smallest undividable functional piece. The composite application developer therefore has to plan for reuse and proper segregation of reusable pieces into a minimal number of DCs. For generic functions, individual DCs should be created to facilitate their reusability and to collect all required elements of the function in this DC.

As a result, parts that are meant for reuse should be put into separate DCs including sufficient definition time for planning the API and separate API implementation. You can add the API to a public part of your DC in these ways:

+   - Choose the DC structure according to its function and not according to the organizational structure of the responsible developers.
+   - Choose the DCs in such a way that the involved developers work in the same team and at the same location. Only if these conditions are met can you use the inactive state of objects, which is mandatory for distributed responsibilities.

These two guidelines seem contradictory, but you should use both guidelines together, so that together they define the minimal structure of DCs.

After a change, you must rebuild the entire DC. You should therefore choose the size carefully so that it does not contain too many objects. This is a very broad statement, so some more details are required.

# Build Time

This section provides more details regarding the general recommendations about how to structure content and what these recommendations look like in the light