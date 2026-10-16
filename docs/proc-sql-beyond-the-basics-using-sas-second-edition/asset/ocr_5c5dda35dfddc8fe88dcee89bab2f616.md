```
/**
            and the last (max) row within each by-group  **/
/**
            using a subquery.                    **/
/****************************************************************/
    create table between_bygroup_rows as
        select custnum,
                prodnum,
                units,
                unitcost,
                min(prodnum) as Min_Prodnum,
                max(prodnum) as Max_Prodnum,
                'BetweenRow' as ByGroup
        from purchases
            group by custnum
            having CALCULATED min_Prodnum NOT =
                    CALCULATED max_Prodnum AND
                    CALCULATED min_Prodnum NOT =
                        prodnum            AND
                    CALCULATED max_Prodnum NOT = prodnum
            order by custnum, prodnum;
/****************************************************************/
/** ROUTINE.....: CONCATENATE-FIRST-BETWEEN-LAST                **/
/** PURPOSE.....: Concatenate the results from the first (min)  **/
/**
                row, between rows, and last (max) row within  **/
/**
                each by-group using UNION ALL set operators. **/
/****************************************************************/
    create table first_between_last_rows as
        select custnum,
                prodnum,
                units,
                unitcost,
                bygroup
        from first_bygroup_rows
    UNION ALL
        select custnum,
                prodnum,
                units,
                unitcost,
                bygroup
        from between_bygroup_rows
    UNION ALL
        select custnum,
                prodnum,
                units,
                unitcost,
                bygroup
        from last_bygroup_rows;
/****************************************************************/
/** ROUTINE.....: PRINT-FIRST-BETWEEN-LAST                      **/
/** PURPOSE.....: Print the results from the first (min) row,   **/
/**
                between rows, and last (max) row within each  **/
/**
                by-group using a select query.                 **/
```