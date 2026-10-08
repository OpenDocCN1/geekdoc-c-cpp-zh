```
else
printf("no value found");
```

or by the use of a null block:

```
if(value found)
  if(value > 0)
{
    s = sqrt(value);
    printf("%f %f"
```

else
printf("no value found");

In the first version, the embedded selection structure is an if...else not an if...else..., the extra set of braces is needed so that the computer knows with which the else belongs. In the second and third versions, problem is avoided by making both of the selection structures of the form...else... even though the inner else has no body of code. Notice that either a semicolon after the first else or empty braces indicate a null branch.

Nested Selection Structure Inside a while Loop Assume candidates A and B are running for office. As the precinct result comes, the votes for each candidate are totaled, the total number of votes are summed. Assume there are 100 precincts.
The code for the flowchart in 4.16 is as follows:

```
int totvote = 0, atot = 0, btot = 0, b;
int num_precincts = 1; /*precincts counter*/
while(num_precincts <= 100) { /*Total number of precincts*/
{
```

```
printf("Enter the number of votes for a and b");
printf("for precinct %d", num_precincts);
sscanf("%d %d", &a, &b);
totvote = totvote + a + b;
atot = atot + a;
btot = btot + b;
if(atot > btot)
```