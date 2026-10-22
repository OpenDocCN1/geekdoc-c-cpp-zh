# 19.3 belongs_to and has_xxx Declarations

The various linkage declarations (belongs_to, has_one, and so on) do more than specify the relationships between tables. They each add a number of methods to the model to help navigate between linked objects. Let’s look at these in more detail. (If you’d like to skip to the short version, we summarize what’s going on in Figure 19.3, on page 386.)

# The belongs_to Declaration

belongs_to declares that the given class has a parent relationship to the class containing the declaration. Although belongs to might not be the first phrase that springs to mind when thinking about this relationship, the Active Record convention is that the table that contains the foreign key belongs to the table it is referencing. If it helps, while you’re coding you can think references but type belongs_to.

The parent class name is assumed to be the mixed-case singular form of the attribute name, and the foreign key field is the lowercase singular form of the parent class name with _id appended. Here are a couple of belongs_to declarations, along with the associated foreign key fields and the target class and table names:

```
class LineItem < ActiveRecord::Base
  belongs_to :product
  belongs_to :invoice_item
end
```

| Declaration in child | Foreign Key | Parent Class | Parent Table |
|---|---|---|---|
| belongs_to :product | product_id | Product | products |
| belongs_to :invoice_item | invoice_item_id | InvoiceItem | invoice_items |

Active Record links line items to the classes Product and InvoiceItem. In the underlying schema, it uses the foreign keys product_id and invoice_item_id to reference the id columns in the tables products and invoice_items, respectively.

You can override these and other assumptions by passing belongs_to a hash of options after the association name:

```
class LineItem < ActiveRecord::Base
  belongs_to :paid_order,
    :class_name => "Order",
    :foreign_key => "order_id",
    :conditions => "paid_on is not null"
end
```

In this example, we’ve created an association called paid_order, which is a reference to the Order class (and hence the orders table). The link is established via the order_id foreign key, but it is further qualified by the condition that it will find an order only if the paid_on column in the target row is not null. In this case, our association does not have a direct mapping to a single column