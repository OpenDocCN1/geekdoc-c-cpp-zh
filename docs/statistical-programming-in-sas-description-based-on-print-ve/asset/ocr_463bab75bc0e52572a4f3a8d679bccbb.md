# 7.9 Appendix: Complete Ohio County Population Data Set

```
/*
Population of Counties by Decennial Census: 1900 to 1990
Compiled and edited by Richard L. Forstall
                Population Division
                US Bureau of the Census
                Washington, DC 20233
*/
data county_pop;
    length char_county $ 10;
    input county6 1-5 pop90 pop80 pop70 pop60 char_county &;
    county = county6-39000;  * removing state id from FIPS;
datalines;
39001    25371    24328    18957    19982 Adams
39003    109755   112241   111144   103691 Allen
39005    47507    46178    43303    38771 Ashland
39007    99821    104215   98237    93067 Ashtabula
39009    59549    56399    54889    46998 Athens
39011    44585    42554    38602    36147 Auglaize
39013    71074    82569    80917    83864 Belmont
39015    34966    31920    26635    25178 Brown
39017    291479   258787   226207   199076 Butler
39019    26521    25598    21579    20857 Carroll
39021    36019    33649    30491    29714 Champaign
39023    147548   150236   157115   131440 Clark
39025    150187   128483   95725    80530 Clermont
39027    35415    34603    31464    30004 Clinton
39029    108276   113572   108310   107004 Columbiana
39031    35427    36024    33486    32224 Coshocton
39033    47870    50075    50364    46775 Crawford
39035    1412140  1498400  1721300  1647895 Cuyahoga
39037    53619    55096    49141    45612 Darke
39039    39350    39987    36949    31508 Defiance
39041    66929    53840    42908    36107 Delaware
39043    76779    79655    75909    68000 Erie
39045    103461   93678    73301    63912 Fairfield
39047    27466    27467    25461    24775 Fayette
39049    961437   869132   833249   682962 Franklin
39051    38498    37751    33071    29301 Fulton
39053    30954    30098    25239    26120 Gallia
39055    81129    74474    62977    47573 Geauga
39057    136731   129769   125057   94642 Greene
39059    39024    42024    37665    38579 Guernsey
39061    866228   873224   924018   864121 Hamilton
39063    65536    64581    61217    53686 Hancock
```