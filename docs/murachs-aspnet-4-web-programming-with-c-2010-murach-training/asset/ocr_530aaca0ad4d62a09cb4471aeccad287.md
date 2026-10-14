# The relationship between the Categories and Products tables

# Primary key

# Foreign key

| CategoryID | ShortName | LongName |
|---|---|---|
| costumes | Costumes | Costumes |
| fx | FX | Special Effects |
| masks | Masks | Masks |
| props | Props | Props |

| ProductID | Name | ShortDescription | LongDescription | CategoryID | ImageFile | UnitPrice | OnHand |
|---|---|---|---|---|---|---|---|
| arm01 | Freddie Arm | Life-size Freddy... | This arm will gi... | props | arm1.jpg | 19.9500 | 200 |
| bats01 | Flying Bats | Bats flying in fr... | Bats flying in fr... | props | cool1.jpg | 69.9900 | 25 |
| bl01 | Black Light (24") | 24" Black light | Create that cree... | fx | blacklight1.jpg | 24.9900 | 200 |
| cat01 | Deranged Cat | 20" Ugly cat | This is one ugly... | props | cat1.jpg | 19.9900 | 45 |
| fog01 | Fog Machine | 600W Fog mac... | The perfect fog... | fx | fog1.jpg | 34.9900 | 100 |
| fogj01 | Fog Juice (1qt) | 1 qt Bottle of fo... | The drink your ... | fx | fogjuice1.jpg | 9.9900 | 500 |
| frankc01 | Frankenstein | Frankenstein co... | It's alive! | costumes | frank1.jpg | 39.9900 | 100 |
| fred01 | Freddie | Freddie Krueger... | The ultimate in ... | masks | freddy1.jpg | 29.9900 | 50 |
| head01 | Michael Head | Mini Michael M... | For classic horro... | props | head1.jpg | 29.9900 | 100 |
| head02 | Saw Head | Jigsaw head sca... | Perfect for getti... | props | head2.jpg | 29.9900 | 100 |
| hippie01 | Hippie | Women's hippi... | Share the peace... | costumes | hippie01.jpg | 79.9900 | 40 |
| jar01 | Jarlar | Jar Jar Binks | Meesa happy t... | costumes | jarjar1.jpg | 59.9900 | 25 |
| martian01 | Martian | Martian costume | Now includes a... | costumes | martian1.jpg | 69.9900 | 100 |
| mum01 | Mummy | Mummy mask | All wrapped up ... | masks | mummy1.jpg | 39.9900 | 30 |
| pow01 | Austin Powers | Austin Powers ... | Be the most sh... | costumes | powers1.jpg | 79.9900 | 25 |
| rat01 | Ugly Rat | 16" Rat | This guy is sure... | props | rat1.jpg | 14.9900 | 75 |
| rat02 | Uglier Rat | 20" Rat | Yuch! This one ... | props | rat2.jpg | 19.9900 | 50 |
| skel01 | Life-size Skeleton | Life-size plastic ... | This blown plas... | props | skell.jpg | 14.9500 | 10 |
| skullfog01 | Skull Fogger | 2,800 cubic foo... | This fogger put... | fx | skullfog1.jpg | 39.9500 | 50 |
| stro01 | Mini-strobe | Black mini stro... | Perfect for crea... | fx | strobe1.jpg | 13.9900 | 200 |
| super01 | Superman | Superman cost... | Look, up in the ... | costumes | superman1.jpg | 39.9900 | 100 |
| tim01 | T&L Machine | Thunder & Lig... | Flash! Boom! Cr... | fx | tim1.jpg | 99.9900 | 10 |
| vader01 | Darth Vader Ma... | The legendary ... | OB1 has taught... | masks | vader1.jpg | 19.9900 | 100 |

# Concepts

+   - The tables in a relational database are related to each other through their key columns. For example, the CategoryID column is used to relate the Categories and Products tables above. The CategoryID column in the Products table is called a foreign key because it identifies a related row in the Categories table.
+   - Usually, a foreign key corresponds to the primary key in the related table. In SQL Server, however, a foreign key can also correspond to a unique key in the related table.
+   - When two tables are related via a foreign key, the table with the foreign key is referred to as the foreign key table and the table with the primary key is referred to as the primary key table.
+   - The relationships between the tables in a database correspond to the relationships between the entities they represent. The most common type of relationship is a one-to-many relationship as illustrated by the Categories and Products tables. A table can also have a one-to-one relationship or a many-to-many relationship with another table.

Figure 12-2 How the tables in a database are related