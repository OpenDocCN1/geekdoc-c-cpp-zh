```
```
21
22 switch( argc ) /* argc conveys the number of arguments */
23 {
24 case 2:
25 {
26 /* Only one param - display as it is */
27 int val = atoi( argv[ 1 ] ); /* Converts ASCII to int */
28 printf ( "%d [dec] = %d [dec]\n", val, val );
29 }
30
31 break;
32
33 case 3:
34 {
35 /* Two params */
36 int val = atoi( argv[ 1 ] );
37 char * base = argv[ 2 ];
38
39 /* For the base, we need to check only its first letter */
40 switch( base[ 0 ] )
41 {
42 case 'h': /* check lowercase */
43 case 'H': /* and uppercase at the same time */
44 /* printf will do the conversion for us */
45 printf ( "%d [dec] = 0x%x [hex]\n", val, val );
46 break;
47
48 case '0':
49 case '0':
50 /* printf will do the conversion for us */
51 printf ( "%d [dec] = 0%o [oct]\n", val, val );
52 break;
53
54
55
56
57 case 'b':
58 case 'B':
59 /* Here we need to do the conversion ourselves */
60 printf ( "%d [dec] = ", val );
61 ToBinConvert( val );
62 printf ( " [bin]\n" );
63
64 break;
65
66
67
68 default:
69 printf ( "Wrong name param. Should be one of: [bin,oct,hex]\n" );
70 break;
71 }
72 }
73
74 }
75
76 break;
77
78
79 default:
80 printf ( "Call with 1 or 2 params.\nCPro dec_val [hex,oct,bin]\n" );
81 break;
82
83 }
```
```