# 168 Oracle SQL Developer Data Modeler for Database Design Mastery Visible

```
)
ORGANIZATION HEAP
NOCCOMPRESS\NNOCACHE
NOPARALLEL
NOROWDEPENDENCIES
DISABLE ROW MOVEMENT
```

```
;
COMMENT ON TABLE "Order" IS 'This is the table for Orders.';
;
PROMPT PRIMARY KEY ON 'Order';
ALTER TABLE "Order"\ADD CONSTRAINT "Order_PK" PRIMARY KEY ("OrderNo") NOT DEFERRABLE
ENABLE VALIDATE;
```

You can also use the preferences to set formatting. In the Preferences dialog, under Data Modeler | SQL Formatter is a parameter called Autoformat SQL and PL/SQL. If you select it, the SQL Format options are applied automatically in the generated PL/SQL code for procedures, packages, views, and triggers. If do not not it, the SQL formatting options are applied only when you request. There are also product-specific formatting options and the Export/Import functionality to share the formatting with other users.

> TIP
Define the Default DDL Files Export Directory setting and you will always know where your DDL files are saved.

![](bbox=[0.097, 0.526, 0.185, 0.563])

> NOTE
Chapter 10 will cover the DDL preferences that affect importing (Replace System Names During Import, Create Domains Import).

![](bbox=[0.097, 0.613, 0.185, 0.65])

Figure 7-2 shows the Preferences dialog open to the Data Modeler | DDL | DDL/Storage tab. The options under DDL Storage Options For Import And Export allow you to define whether the storage options will be included in the DDLs for import and export operations. You can include or exclude these parameters from the storage clause in DDL: PCTFREE, PCTUSED, INITRANS and MAXTRANSANS, INITIAL, NEXT, MINEXTENTS, MAXEXTENTS, PCTINCREASE, BUFFER_POOL, FREELIST, FREELIST GROUPS, OPTIMAL, and Encryption. The default behavior is that all these keywords are selected, and the values defined in the physical model are included for them in the generated DDL.