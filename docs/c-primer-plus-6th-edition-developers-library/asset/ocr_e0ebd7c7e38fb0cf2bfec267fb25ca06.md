+   4. a. scanf("%d", &x) == 1
+   b. x != 5
+   c. x >= 20

5. Line 4: Should be list[10].
Line 6: Commas should be semicolons.
Line 6: The range for i should be from 0 to 9, not 1 to 10.
Line 9: Commas should be semicolons.
Line 9: >= should be <=. Otherwise, when i = 1, the loop runs for quite a while.
Line 10: There should be another closing brace between lines 9 and 10. One brace closes the compound statement, and one closes the program. In between should be a return 0; line.

Here's a corrected version:

```
#include <stdio.h>
int main(void)
{
	int i, j, list[10]; /* line 3 */
	for (i = 0; i < 10; i++) /* line 6 */
	{
		list[i] = 2*i + 3; /* line 7 */
		for (j = 1; j <= i; j++) /* line 8 */
			printf("%d", list[j]); /* line 9 */
		printf("\n"); /* line 10 */
	}
	return 0;
}
```

6. Here's one way:

```
#include <stdio.h>
int main(void)
{
	int col, row;
	for (row = 1; row <= 4; row++)
	{
		for (col = 1; col <= 8; col++)
		{
			printf("$");
		}
		printf("\n");
	}
}
```