```
proc sql;
    select * from m1d;
    select * from m2d;
    select *
        from m1d, m2d
        where m1d.id=m2d.id;
```