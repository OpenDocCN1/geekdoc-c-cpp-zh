# Chapter 5: Predefined Packages 105

The after-reset report shows all went as planned.

Figure 5.19: Sample of the Data After Restoration with the SQLSTMT Package
crs.Prices After Reset

| Row | product_id | PRICE |
|---|---|---|
| 1 | 210200100009 | $34.70 |
| 2 | 220200100012 | $58.70 |
| 3 | 230100500006 | $8.40 |
| 4 | 240100100366 | $16.30 |
| 5 | 240500100039 | $34.50 |
| 6 | 240800200063 | $36.90 |

210200100009 and 240800200063 Should Not Be Updated
Original Prices were $34.70 and $36.90

And the audit trail was updated to reflect the additional changes.

Figure 5.20: Audit Data Set After SQLSTMT Package Restoration Process Executed
Price Change Audit Trail

| Row | Changed_On | Changed_By | Prod_ID | Original_Price | Updated_Price |
|---|---|---|---|---|---||
| 1 | 16JAN16:11:37:08 | Student | 220200100012 | $58.70 | $61.64 |
| 2 | 16JAN16:11:37:08 | Student | 230100500006 | $8.40 | $8.82 |
| 3 | 16JAN16:11:37:08 | Student | 240100100366 | $16.30 | $17.12 |
| 4 | 16JAN16:11:37:08 | Student | 240500100039 | $34.50 | $36.23 |
| 5 | 16JAN16:11:37:08 | Student | 240500100039 | $36.28 | $34.50 |
| 6 | 16JAN16:11:37:08 | Student | 230100500006 | $8.90 | $8.40 |
| 7 | 16JAN16:11:37:08 | Student | 220200100012 | $61.83 | $58.70 |
| 8 | 16JAN16:11:37:08 | Student | 240100100366 | $17.03 | $16.30 |

210200100009 and 240800200063 Should Not Be Updated
Original Prices were $34.70 and $36.90