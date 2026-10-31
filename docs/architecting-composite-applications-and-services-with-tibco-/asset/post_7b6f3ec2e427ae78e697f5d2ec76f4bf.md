
sequencing key whose value is an xpath expression that yields a value. Within an engine, messages for which this value is the same are guaranteed to be processed in the sequence received. In the bank account example, if the xpath expression references the account number, then all messages with a given account number will be processed in the order received. 3

## Two-Tier Load Distribution Preserving Partial Ordering

When you need to preserve partial-order sequencing and distribute load, you can use a two-tier load distribution pattern (Figure 11-13). This pattern requires workers to individually preserve partial ordering of their work. The work is then distributed among the workers by a dispatcher that preserves partial ordering; that is, it always distributes work associated with a specific entity to the same worker.

## Implementing Two-Tier Load Distribution Preserving Partial Ordering

The two-tier load distribution pattern that preserves partial ordering can be implemented in ActiveMatrix Service Bus using ActiveMatrix BusinessWorks for the workers (Figure 11-14) and the Mediation implementation type for the dispatcher. The dispatcher uses a Custom Mediation Task that accepts the value identifying the entity (i.e., the result of the xpath expression) and uses a hash function to determine which worker should get this particular request. Each worker has its own JMS queue to which the dispatcher sends the requests. The processes implemented in BusinessWorks similarly use the same xpath expression for their sequencing key.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_315_0.png)

Figure 11-13: Two-Tier Load Distribution Preserving Partial Ordering

3. At the time of this writing, a sequencing key was not yet available for processes initiated by the Service activity from the Service palette.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_316_0.png)

Figure 11-14: Implementing Two-Tier Load Distribution Preserving Partial Ordering

For this pattern to work, there are a number of additional constraints that need to be followed. The service client must use a JMS transport, either XML over JMS or SOAP over JMS, to submit requests. The dispatcher must be in its own ActiveMatrix node and the JMS Binding Pool size on that node must be set to 1. The ActiveMatrix BusinessWorks processes must use the SOAP Event Source activity from the SOAP palette as the process starter and use the sequencing key of this activity.⁴

## Summary

When the volume of work exceeds the capacity of a single component, that work must be distributed among multiple workers. One common

4. If a sequencing key becomes available on the Service activity of the Service palette, it could be used in this pattern as well.

This page intentionally left blank

## Chapter 12

## Data Management Patterns

## Objectives

Data plays a key role in business processes. As such, you need to carefully consider how that data is managed. At the most concrete level, you need to consider where individual pieces of data reside and whether or not they are replicated in different components. Broadly speaking, there are five patterns that can be used for data management:

- 1. System of Record
- 2. System of Record with Cached Read-Only Copies
- 3. Replicated Data with Transactional Update
- 4. Edit Anywhere Reconcile Later
- 5. Master Data Management

The following sections explore these patterns. After reading this chapter you will be able to describe these five data management patterns and the pros and cons of each.

## System-of-Record Pattern

The simplest data management pattern is to have a single system of record (Figure 12-1). All data resides in a single system, and any component that uses or modifies the data uses that system's data access interface to read or update the information. From a data management perspective, this is the simplest approach. All of the logic needed to maintain the consistency of the data resides in the system of record.

This pattern is rarely found in the enterprise, for a variety of reasons, both conceptual and practical. At the conceptual level, a single system of record may have difficulty scaling; There may be too much data and too much access activity for one system to practically manage all of it. The use of this pattern may also introduce a reliability problem: If the system of record is down, or network problems prevent access to it, no work can be accomplished.

Having said this, there are emerging technologies that are beginning to make this pattern viable. TIBCO ActiveSpaces™, for example, can manage large datasets (in excess of a terabyte) in memory and distributed across many machines with built-in redundancy management (i.e., fault tolerance). These same capabilities are available in TIBCO BusinessEvents.

At the practical level, enterprises tend to acquire commercial off-the-shelf (COTS) software packages to support different parts of their operations. An order management package might be acquired to handle sale orders and a fulfillment package to handle shipments. Each of these packages manages its own set of data, but there is usually some overlap. To the extent that each piece of data resides in only one of these packages, you still have the System-of-Record pattern. However, if there is replicated data, the System-of-Record pattern does not apply. A fulfillment package, for example, typically contains some information about the

![](img/b8d8132a583ad73d511c4c1bb92e2df7_320_0.png)

Figure 12-1: Single System-of-Record Pattern

## DAG 编写最佳实践

在 DAG 中创建新任务或编写新的 DAG 时，您应当记住以下最佳实践，使 DAG 更稳定、清晰且易于维护。

### 创建 Airflow 连接

创建 Airflow 连接时，请使用连接 ID 标识连接。在 DAG 中使用相同连接时，避免使用不同参数重复创建同一连接，否则会让连接配置变得难以跟踪。

```python
from airflow.models import Connection
from airflow.settings import Session

conn = Connection(
    conn_id="my_prod_db",
    conn_type="postgres",
    host="postgres.internal.example.com",
    login="airflow",
    password="secret",
    schema="analytics",
)

Session.add(conn)
Session.commit()
```

> > **注意**：连接应在系统中的任何 DAG 运行之前只创建一次。不要使用同一个 `conn_id` 和不同参数创建多个连接。

- 为每个租户或环境使用独立的连接
- 不要在同一 DAG 中重复定义相同的连接
- 在自定义 hooks / operators 中使用上下文管理器来管理连接生命周期

required to maintain consistency. It is common to “instrument” these systems to detect data changes and update other systems.

This most common occurrence of this pattern involves reference data (customer, partner, product, etc.) that typically appears in many systems. This is also information for which inconsistencies may cause significant business problems. To minimize the inconsistencies and resolve them when they occur, the preferred approach to maintaining distributed reference data is to use the Master-Data-Management pattern.

## Master-Data-Management Pattern

The problem of minimizing, identifying, and reconciling inconsistencies among multiple sources is particularly important for reference data (e.g., information about customers, products, and partners). As the previous discussion of the Edit-Anywhere-Reconcile-Later pattern made clear, simply publishing the changes and having other systems subscribe to those changes and update their data cannot ever guarantee consistency and does nothing to resolve inconsistencies should they arise.

The Master-Data-Management pattern (Figure 12-5) is commonly employed to address this problem. The master data manager defines

![](img/b8d8132a583ad73d511c4c1bb92e2df7_324_0.png)

**Figure 12-5:** *Master-Data-Management Pattern*

a consolidated data model encompassing the reference data distributed across all of the systems. It also defines mappings of each system's subset of master data into that model. This model is used for several purposes.

One of the purposes is to aid in maintaining the data in the individual systems containing master data. Each of these systems has two interfaces: a notification interface that is used to inform the master data manager that changes have occurred, and an update interface that is used to update information when changes occur elsewhere. When a change occurs in one system, the master data manager maps the change into the consolidated data model and then uses the mappings to the other systems to update their data as required. Note that these two interfaces may be add-ons to the underlying systems in the form of service wrappers or adapters.

Another purpose of the consolidated model is to present a comprehensive logical view to components requiring access to master data. This not only provides a uniform view of the data but also isolates the components from the details of the underlying systems. In some variations of the pattern this view is strictly for queries. In other variations it may be used to update the master data as well. It is worth noting that some master data management products can only support a low volume of activity on this interface. As such, the view they present is not well suited to providing this information for use in high-volume transactional business processes.

Despite the presence of the master data manager, discrepancies can still arise, if for no other reason than the data was inconsistent initially. Thus an important aspect of a master data manager is an interface through which discrepancies can be identified and resolved. This is typically a human interface, since in most cases someone will have to investigate in order to determine which of the conflicting values is correct.

The TIBCO Collaborative Information Manager is designed to play the master data manager role in this pattern. It supports the definition of the consolidated data model and its mapping to the subsets found in individual systems. It enables the definition of processes for handling data change and discrepancy resolution. It also provides a query interface that can support a high-volume of activity and thus support transactional business processes that require access to reference data.
