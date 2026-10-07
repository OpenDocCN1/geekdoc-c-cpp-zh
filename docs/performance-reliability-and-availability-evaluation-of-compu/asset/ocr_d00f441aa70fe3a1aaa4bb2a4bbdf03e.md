Workload Characterization

447

In this chapter, we classify the computer workloads into three main classes, here
The second is subdivided into two sub-classes:

+   - Real Workload
- Synthetic Workload
  - Benchmarks
  - Synthetic Operational Workload
- Performance Workload Model

A real workload is a timely ordered set of requests, transactions, program execu-
tions, and tasks carried out by a computer system during a production period of in-
ter. By production period, we mean the time interval a computer system executes
its ordinary, everyday, common tasks during a window of particular
concern. This workload indeed represents the computer system real load demand
that occurred in that specific time. The computer load changes from hour-
hour, weekday to weekday, and season to season; however, a fundamental task for gathering-representative data is the definition of the measuring period and the sampling
frequency. The sampling frequency is a key concern when a sampling strategy is ad-
opt instead of a complete record of activities during the production period.

As an example, consider an application-workload related to an online drugstore
sales system. For the sake of simplicity, let us assume only on non-prescription medi-
cines. From the perspective of customer sales, assume this system supports three
sorts of transactions; the first consists of customers consulting the availability of the
product. Customers are depicted in Figure 24.1. Second, suppose the medicine is not
available (checked in the computer infrastructure database - see Figure 24.1). In that
case, the online sales system reports informing that the drugstore does not have the
required item.

On the other hand, the sales system shows the item, price, and number of items
available in the stock. After that, the customer may add the item to its cart and start
a new consulting transaction or leave the website. A second transaction type is pay-
ing transactions. Suppose the customer (after inserting items in its cart) decides to
purchase the items. In that case, the customer should provide the card data (let us
assume only this option for simplicity) and the delivery address. Then, the sales
processes the selling transaction by consulting the responsive card flag company
(see Figure 24.1). If the credit card allows the transaction, the drugstore
receives proof of purchase with the confirmed delivery address.

Each server of the system infrastructure (web-servers, application servers, database-server, load-balancer) supports their specific purpose applications (denoted by App);
alalso, has a set of monitoring applications (represented by M). The monitoring