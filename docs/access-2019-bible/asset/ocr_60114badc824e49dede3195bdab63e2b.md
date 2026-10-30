relationships easy to establish, if a few rules are followed. These rules are explained in various places in this book. For example, in order to update either side of a many-to-many relationship (for example, to change club membership for a student), the join table must contain the primary keys of both tables joined by the relationship.

Many-to-many relationships are common in business environments:

+   - **Lawyers to clients (or doctors to patients):** Each lawyer may be involved in several cases, while each client may be represented by more than one lawyer on each case.
+   - **Patients and insurance coverage:** Many people are covered by more than one insurance policy. For example, if you and your spouse are both provided medical insurance by your employers, you have multiple coverage.
+   - **Video rentals and customers:** Over a year’s time, each video is rented by several people, while each customer rents more than one video during the year.
+   - **Magazine subscriptions:** Most magazines have circulations measured in the thousands or millions. Most people who subscribe to a magazine, subscribe to more than one at a time.

The Collectible Mini Cars database has a many-to-many relationship between tblCustomers and tblSalesPayments, linked through tblSales. Each customer might have purchased more than one item, and each item might be paid for through multiple payments. In addition to joining contacts and sales payments, tblSales contains other information, such as the sale date and invoice number. The join table in a many-to-many relationship often contains information regarding the joined data.

As shown in Figure 4.13 join tables can contain information other than the primary keys of the tables they join. The tblStudentToClubJoin table includes a field to record the date that the related student joined the related club.

# Integrity Rules

Access permits you to apply referential integrity rules that protect data from loss or corruption. Referential integrity means that the relationships between tables are preserved during updates, deletions, and other record operations. The relational model defines several rules meant to enforce the referential integrity requirements of relational databases. In addition, Access contains its own set of referential integrity rules that are enforced by the ACE database engine.

Imagine a payroll application that contained no rules regulating how data in the database is used. It would be possible to issue payroll checks that aren’t linked to an employee, for instance. From a business perspective, issuing paychecks to “phantom” employees is a very serious situation. Eventually, the issue will be noticed when the auditors step in and notify management of the discrepancy.

Referential integrity operates strictly on the basis of the tables’ key fields. Referential integrity means that the database engine checks each time a key field (whether primary