constraints, in which case your statement should look like this:

```
SET CONSTRAINTS ALL DEFERRED
```

Once you have completed operations on the database, you can then choose to apply the changes. In that case, the statement will look like this:

```
SET CONSTRAINT ALL IMMEDIATE
```

So through this chapter, you have understood the idea behind SQL transactions, and why they are essential when working with SQL programming.