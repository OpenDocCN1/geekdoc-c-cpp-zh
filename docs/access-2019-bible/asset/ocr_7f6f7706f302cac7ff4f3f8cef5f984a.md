# TABLE 1.3 (continued)

| Customer Data | Invoice Data | Line Items | Payment Information |
|---|---|---|---|
| zip code | Tax Rate | Discount for Each Item | Expiration Date |
| Phone Numbers (two fields) |  | Taxable? |  |
| E-Mail Address |  |  |  |
| Web Address |  |  |  |
| Discount Rate |  |  |  |
| Customer Since |  |  |  |
| Last Sales Date |  |  |  |
| Sales Tax Rate |  |  |  |
| Credit Information (four fields) |  |  |  |

Consolidating and comparing data is a good way to start creating the individual table, but you have much more to do.

As you learn more about how to perform a data design, you also learn that the customer data must be split into two groups. Some of these items are used only once for each customer, while other items may have multiple entries. An example is the Sales column—the payment information can have multiple lines of information.

You need to further break these types of information into their own columns, thus separating all related types of items into their own columns—an example of the normalization part of the design process. For example, one customer can have multiple contacts with the company or make multiple payments toward a single sale. Of course, we've already broken the data into three categories: customer data, invoice data, and line-item details.

Keep in mind that one customer may have multiple invoices, and each invoice may have multiple line items on it. The invoice-data category contains information about individual sales and the line-items category contains information about each invoice. Notice that these three columns are all related; for example, one customer can have multiple invoices, and each invoice may require multiple line items.

The relationships between tables can be different. For example, each sales invoice has one and only one customer, while each customer may have multiple sales. A similar relationship exists between the sales invoice and the line items of the invoice.

Database table relationships require a unique field in both tables involved in a relationship. A unique identifier in each table helps the database engine to properly join and extract related data.