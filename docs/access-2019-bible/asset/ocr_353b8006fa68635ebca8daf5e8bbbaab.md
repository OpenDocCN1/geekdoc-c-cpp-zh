# Part V: Working with Access Forms and Reports

There are many situations where aggregate information provides valuable insight into data analysis. Consider a report that must contain each salesperson’s performance over the last year measured against the total sales for the sales organization, or a region’s sales figures against sales for the entire sales area. A bookstore might want to know what portion of its inventory is devoted to each book category.

Figure 21.41 shows such a report. The Number of Customers, Total Sales, and Average Purchase information at the top of this report (rptSummary) are all part of the report header. In a one-pass report writer, the data needed to perform these calculations would not appear until the bottom of the page, after all the records have been processed and laid out.

# FIGURE 21.41

The summary information is part of the report’s header.

![](bbox=[0.18, 0.55, 0.66, 0.88])

A glance at rptSummary in Design view (see Figure 21.42) reveals that the text boxes in the report header are populated with data derived from these mathematical expressions:

```
Number of Customers: =Count([CompanyName])
Total Sales: =Format(Sum([Purchases]),"Currency")
Average Purchase: =Format(Sum([Purchases]) / Count([CompanyName]), "Currency")
```