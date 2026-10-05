Sec. 10.1 Linear Indexing

355

| | AA10 | AB12 | AB39 | FF37 |
|---|---|---|---||
| Smith | AX33 | AX35 | | |
| Zukowski | ZQ99 | | | |

**Figure 10.3** A two-dimensional linear index. Each row lists the primary keys associated with a particular secondary key value. In this example, the secondary key is a name. The primary key is a unique four-character code.

| Secondary Key | Primary Key |
|---|---|n| Jones | AA10 |
| Smith | AB12 |
| Zukowski | AB39 |
| | FF37 |

![](bbox=[0.373, 0.331, 0.627, 0.546])

**Figure 10.4** Illustration of an inverted list. Each secondary key value is stored in the secondary key list. Each secondary key value on the list has a pointer to a list of the primary keys whose associated records have that secondary key value.

Consider a large database of employee records. If the primary key is the employee's ID number and the secondary key is the employee's name, then each record in the name associates a name with one or more ID numbers. The ID number index turn associates an ID number with a unique pointer to the full record on disk. The secondary key index in such an organization is also known as an *inverted list* or *inverted file*. It is inverted because searches work backwards from the secondary key to the primary key to the actual data. It is called an inverted list because each secondary key value has (conceptually) a list of primary keys associated with it. Figure 10.4 illustrates this arrangement. Here, we have last names as the secondary key. The primary key is a four-character unique identifier.

Figure 10.5 shows a better approach to storing inverted lists. An array of secondary key values is shown as before. Associated each secondary key is a pointer to an array of primary keys. The primary key array uses a linked-list implementation. This approach combines the storage for all of the secondary key lists into a single array, probably saving space. Each record in this array consists of a