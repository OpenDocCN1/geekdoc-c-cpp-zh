# Multiple-Query Processing and Optimization Techniques ■ 163

significant paradigm shift to make configuring applications simple and easy for the customers, without incurring extra operation costs.

In the following, we discuss the extensions of the above multiple-query processing and optimization techniques to the domain of multitenant databases.

# 7.4.1 Sharing in Multitenant Query Processing

Queries for a single tenant have to contend with data from all tenants. However, previous query methods have been inefficient for multitenant databases because it is very difficult for such methods to understand or account for the unique characteristics of each tenant's data. While one tenant's data includes numerous short records with fewer indexable fields, another may fewer longer records with numerous index fields [44]. Apart from the structural differences, each tenant's data distribution may also be different with the similar schemas. This brings a challenge for existing relational databases that gather an aggregate or average statistics of all tenants periodically. Therefore, the approach to MQO can lead to incorrect assumptions and query plans for any given tenant.

A natural way to ameliorate the problem is to share tables among tenants [45,46]. Through mapping multiple single-tenant logical schemas to one multitenant physical schema using query transformation rules, the logical tables can be divided into generic structures, such as universal and pivot tables, to avoid the interference with each tenant's ability. For each table, queries are generated to filter the correct columns and align the different chunks based on each TenantId. Then shared process offer execution of administrative queries by allowing them to be parameterized over the domain of each table.

In addition, each tenant database may encounter various expressions such as relational and structured XML data. Therefore, a multigraph-based approach is proposed to introduce edges that navigate both the XML nodes and the relational data notations. Through utilizing the intragment compression techniques and adding new edges, similar nodes can form a subgraph that consists of identical or subsumed conditions.

# 7.4.2 Multitenant Querying Plans

More efficient execution plans of multitenant databases are to adopt a two-phase solution with dynamic tuning of database indices [47]. A layer