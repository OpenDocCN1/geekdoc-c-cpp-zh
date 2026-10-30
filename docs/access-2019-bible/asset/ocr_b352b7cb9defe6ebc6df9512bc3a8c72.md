# FIGURE 4.11

A one-to-one relationship.

![](bbox=[0.12, 0.225, 0.68, 0.595])

There are times, however, when storing certain data along with other data in the table isn’t a good idea. For example, consider the situation illustrated in Figure 4.11. The data contained in tblSecurityIDs is confidential. Normally, you wouldn’t want anyone with access to the public customer information (name, address, and so on) to have access to the confidential security code that the customer uses for purchasing or billing purposes. If necessary, tblSecurityIDs could be located on a different disk somewhere on the network, or even maintained on removable media to protect it from unauthorized access.

Another instance of a one-to-one relationship is a situation known as subtyping. For example, your database may contain a Customers table and a Vendors table. If both your customers and vendors are businesses, a lot of the information for both entities may be similar. In that case, you may prefer to have a Companies table that contains all the data that is similar, such as CompanyName, Address, and TaxIdentificationNumber. Then your Customers and Vendors table would contain a reference to the Companies table and include additional fields that are particular to customers and vendors, respectively. The customer and vendor entities are subtypes of the companies and related one-to-one.

A common situation for one-to-one relationships is when data is being transferred or shared among databases. Perhaps the shipping clerk in an organization doesn’t need to see all of a customer’s data. Instead of including irrelevant information—such as job titles, birth dates, alternate phone numbers, and e-mail addresses—the shipping clerk’s database contains only the customer’s name, address, and other shipping information. A record in