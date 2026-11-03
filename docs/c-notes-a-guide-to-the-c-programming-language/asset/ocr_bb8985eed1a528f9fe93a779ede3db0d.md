Furthermore, the size of the outer array may be implicitly given by the size of an initializer-list as in

```
float vector[] = {0.1, 0.2, 0.3, 0.4};
```

which is identical to the same declaration with vector[4]. Only the left-most array size specification should be empty, as in

```
int matrix[][3] = {{1}, {2, 3}, {4}};
```

which is once again equivalent to the above. Auto arrays may not be initialized; separate scalar assignments must be made in the function body.

# 2.5 Structure initializers

The structure initializer, like an array initializer, has the following form:

```
= _opt_ expr | { initializer-list , _opt_ }
```

where the expr initializes only the first element or where each initializer of the list taken in order must be a valid initializer for the corresponding part of the structure; parts are in the same order as given by the structure declaration. For example,

```
struct node {int degree; char name[5];
float weight; struct node *next;};

struct node first_node =
{2, "Node", 3.7E4, &other_node};
```

These declarations make first_node a variable of type struct node and initialize the parts, as follows:

| first_node.degree | is | 2 |
| first_node.name | is | "Node" or {'N','o','d','e','\0'} |
| first_node.weight | is | 3.7E4 |
| first_node.next | points at | other_node |

A more complicated example is

```
struct {COMPLEX matrix[2][2]; char tag;}
cmat =
{/* first the matrix */
{
{[-1, 0], [0, 1]}, /* row 0 */
{[-3.2, 5.]}, /* row 1 */
},
/* then the tag */
'M'
};
```