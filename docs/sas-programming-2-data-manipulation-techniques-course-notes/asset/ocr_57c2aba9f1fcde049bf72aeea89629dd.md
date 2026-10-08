# Completed Business Scenario

```
data correct;
set orion.clean up;
if find(tranwrd, 'Mittens', 'I') > 0 then do;
substr(Product_ID, 9, 1) = '5';
Product=tranwrd(Product, 'Luci ,'Lucky');
end;
Product_ID=compress(Product_ID);
Product=popcase(Product);
run;
```

| Product_ID | Product | Order_ID |
|---|---|--|
| 21020200003 | Sunfit Trunks, Blue | 1231986335 |
| 21020050003 | Lucky Mittens, Red | 1232003930 |
| 21020050004 | Lucky Mittens, Blue | 1232007693 |
| 21020200004 | Sunfit Trunks, Aqua | 1232007700 |

# COMPRESS Function: Example

The COMPRESS function removes the characters listed in the chars argument from the source.

```
ID='20 01-005 024';
New ID1=compress(ID);
New ID2=compress(ID, '-');
New ID3=compress(ID, '-');
```

| PDV | ID | New_ID1 |
|---|---|--|
| | $ 13 | $ 13 |
| 20 01-005 024 | | 200100024 |

| New_ID2 | New_ID3 |
|---|--|
| $ 13 | $ 13 |
| 20 01-005 024 | 2001005024 |