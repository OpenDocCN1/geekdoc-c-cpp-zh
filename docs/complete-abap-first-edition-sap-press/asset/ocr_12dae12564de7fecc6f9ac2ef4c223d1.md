| ITEM_ID | LANGUAGE | DESCRIPTION | QUANTITY | UOM |
|---|---|---|---|---|
| 1 | English | Pen | 10 | PC |
| 1 | German | Stift | 10 | PC |
| 2 | English | Pencil | 20 | Box |
| 2 | German | Bleistift | 20 | Box |
| 3 | English | Paper | 10 | KG |
| 3 | German | Papier | 10 | KG |

**Table 2.3** TB_ITEM Expanded to Accommodate Language Key

In Table 2.3, the ITEM_ID field is no longer unique. The primary key of the table should always be unique, so the key of this table should be expanded to include the LANGUAGE field as well. Therefore, the key of Table 2.3 is a combination of the ITEM_ID and LANGUAGE fields. Individually, the data in ITEM_ID field can repeat n number of times and the data in LANGUAGE field can repeat n number of times, but the combination should always be unique.

As you may have noticed, in Table 2.3 we're repeating the same data multiple times to accommodate various languages. When more languages are added to the mix, you end up with redundant data. What if we could separate the descriptions and maintain them in a separate table that can be linked to this table with foreign keys?

Table 2.4 stores the item details, and Table 2.5 stores the descriptions in multiple languages. This arrangement of tables avoids data redundancy, and because the tables are now linked through a foreign key, we can query Table 2.5 for the description in the preferred language using the ITEM_ID field of Table 2.4.

| ITEM_ID | QUANTITY | UOM |
|---|---|---|
| 1 | 10 | PC |
| 2 | 20 | Box |
| 3 | 10 | KG |

**Table 2.4** TB_ITEM without Description