# 156 Cloud Computing and Digital Media

![](bbox=[0.125, 0.098, 0.874, 0.373])

FIGURE 7.2 MQO in streaming databases. PPD, partial push-down; DSF, shared data fragment; SDS, shared data shard; STS, shared time slice.

# 7.3.1 Identifying Shared Computation for Continuous Queries

In contrast to traditional sharing strategy of just finding common sub-expressions in nonstreaming systems, MQO in streaming databases has generally been accomplished through "indexing" potentially large sets of queries to efficiently process the incoming data. Different approaches are developed to cope with different types of streaming queries.

**Join queries with no aggregate operators.** These kinds of queries are identical except for individual predicates. Continuous adaptive continu-ous processing (CACQ) [27] proposes a solution of using the eddy to route tuples among all the continuous queries currently in the system. Eddy [28] is a typical query processing mechanism, which continuously reorders the application of pipelined operators in a query plan based on tuple-by-tuple granularity. Each tuple is extended to carry the "lineage" consisting of "steering" and "completion" vectors in the memory. Through encoding the work performed on a tuple's length, the operators from many queries can be applied in a single tuple. Meanwhile, an efficient predicate index called group filter is applied to reduce computation when selection predicates havealities. For instance, when a selection operator is inserted into a new query, its source field is checked whether it matches an already instantiated group filter. If the requirements are met, predi-cate is merged into the filter; otherwise, a new filter will be created with a single predicate. To avoid redundancy, the scheme splits joins into unary