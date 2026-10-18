Table A.2. Common C string functions (in <string.h>). The C++ SL contains their counterparts - the same names with the std:: prefix (in <string>).

Object Description Examples
strlen Returns the length of a C string pointed to by s (the sentinel 0 is not counted).
int strlen( const char * s );
A few operations on C strings:
1 char s1[] = "Quick fox";
2 char s2[] = "fox";
4 /* Output length of both strings */
5 printf ("%len(s1)=%d, len(s1)=%d\n", strlen( s1 ), strlen( s2 ) );
8 /* Check if strings are the same */
9 printf( "cmp(s1,s2)=%d\n", strcmp( s1, s2 ) );
11 char s3[ 64 ] = "\0"; /\* large buffer, empty string \*/
12 strcpy( s3, s1 ); /\* Copy s1 to s3 */
13 printf ( "cmp(s1,s2)=%d\n", strcmp( s1, s3 ) );
15 strcat( s3, " jumped" ); /\* Join two strings \*/
16 printf ( "s3=%s\n", s3 );
18 /* Find if s2 is part of s1 */
19 printf ( "s2 is a part of s1: %s\n", strstr( s1, s2 ) != NULL ? "yes" : "no" );
(Continued)