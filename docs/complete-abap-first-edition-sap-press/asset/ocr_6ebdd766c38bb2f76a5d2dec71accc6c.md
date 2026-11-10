Listing 5.18 demonstrates using the `READ` statement with a free key, table key, and index. When reading an internal table record using an index, the system uses the index of the primary key by default.

If you want to use the index of the secondary key, you can explicitly specify the secondary key name via the `USING KEY` addition. If you specify a primary key after the `USING KEY` addition, then the behavior is similar to using the `READ` statement without the `USING KEY` addition.

The `LOOP` statement can be used to process multiple rows. The system loops between `LOOP` and `ENDLOOP`, reading one row at a time to the work area.

Listing 5.19 shows the syntax to use the `LOOP` statement.

```
```
*Looping all the records of the internal table
LOOP AT it_sflight INTO wa_sflight.
*Statements to process the row can go here
ENDLOOP.
*Looping specific records of the internal table using key
LOOP AT it_sflight INTO wa_sflight WHERE connid EQ '0004'.

ENDLOOP.
*Looping specific records using secondary key. Assuming a
*secondary key "by_airline" is defined with carrid and connid as
*components.
LOOP AT it_sflight INTO wa_sflight
        USING KEY by_airline
        WHERE carrid EQ 'AA'
        AND connid EQ '0004'.

ENDLOOP.
*Looping specific records using index.
LOOP AT it_sflight INTO wa_sflight FROM 3 TO 5.

ENDLOOP.

*Looping specific records using secondary key index. Note that
*the secondary key should be a sorted key and not hashed key
LOOP AT it_sflight INTO wa_sflight USING KEY by_airline
        FROM 3 TO 5.

ENDLOOP.
```
```

**Listing 5.19** Using LOOP Statement

Listing 5.19 demonstrates different scenarios to use the `LOOP` statement to process the internal table records. You can loop all the records of the internal table or