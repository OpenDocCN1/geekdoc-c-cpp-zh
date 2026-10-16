| Column | Type | Length | Format | Informat | Label |
|---|---|---|---|---|---|
| Nobs | num |  |  |  | # of Obs |
| Obslen | num |  |  |  | Obs Length |
| Nvar | num |  |  |  | # of Variables |
| Protect | char | 3 |  |  | Type of Password Protection |
| Compress | char | 8 |  |  | Compression Routine |
| Encrypt | char | 8 |  |  | Encryption |
| Npage | num |  |  |  | # of Pages |
| Pcompress | num |  |  |  | % Compression |
| Reuse | char | 3 |  |  | Reuse Space |
| Bufsize | num |  |  |  | Bufsize |
| Delobs | num |  |  |  | # of Deleted Obs |
| Indxtype | char | 9 |  |  | Type of Indexes |
| Datarep | char | 32 |  |  | Data Representation |
| Reqvector | char | 24 | $HEX. | $HEX. | Requirements Vector |

# Table 2.11: DICTIONARY.TITLES or SASHELP.VTITLE

| Column | Type | Length | Label |
|---|---|---|---|
| Type | char | 1 | Title Location |
| Number | num |  | Title Number |
| Text | char | 256 | Title Text |

# Table 2.12: DICTIONARY.VIEWS or SASHELP.VVIEW

| Column | Type | Length | Label |
|---|---|---|---|
| Libname | char | 8 | Library Name |
| Memname | char | 32 | Member Name |
| Memtype | char | 8 | Member Type |
| Engine | char | 8 | Engine Name |

# Accessing a Dictionary Table’s Contents

The content of a dictionary table is accessed with the SQL procedure’s SELECT statement FROM clause. Results are displayed as rows and columns in a table, and can be used in handling common data processing tasks including obtaining a list of allocated libraries, catalogs and data sets, as well as communicating SAS environment settings to custom software applications. Users should take the time to explore the capabilities of these read-only dictionary tables and become familiar with the type of information they provide.