value, and ReleaseStringUTFChars to inform the virtual machine that access to the string is no longer required.

# Listing 12.10  `printf2/Printf2.c`

```
/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */

#include "Printf2.h"
#include <string.h>
#include <stdlib.h>
#include <float.h>

/**
 * @param format a string containing a printf format specifier
 *        (such as "%.2f"). Substrings "%%" are skipped.
 * @return a pointer to the format specifier (skipping the '%')
 *         or NULL if there wasn't a unique format specifier
 */
char* find_format(const char format[])
{
   char* p;
   char* q;

   p = strchr(format, '%');
   while (p != NULL && *(p + 1) == '%') /* skip %% */
      p = strchr(p + 2, '%');
   if (p == NULL) return NULL;
   /* now check that % is unique */
   p++;
   q = strchr(p, '%');
   while (q != NULL && *(q + 1) == '%') /* skip %% */
      q = strchr(q + 2, '%');
   if (q != NULL) return NULL; /* % not unique */
   q = p + strspn(p, "0-# "); /* skip past flags */
   q += strspn(q, "0123456789"); /* skip past field width */
   if (*q == '.') { q += strspn(q, "0123456789"); }
      /* skip past precision */
   if (strchr("eEfFgG", *q) == NULL) return NULL;
      /* not a floating-point format */
   return p;
}

JNIEXPORT jstring JNICALL Java_Printf2_sprint(JNIEnv* env, jclass cl,
         jstring format, jdouble x)
{
```