# ARRAYS

Just like visualizing a 2-D array as a matrix, a 3-D array can be visualized
as 'n' 2-D arrays, where n is the first subscript value.
For example:

+   * int a[3][2][2]; 3*2*2 arrays are declared.
* float b[2][3][3]; 2*3*3 arrays are declared.

# 3.5.2. Initializing a 3-D array

+   * While declaration,
int a[3][2][2]={1,1,1,1],[2,2,2,2],[3,3,3,3]];

+   * At a later point in program (using loops)
for(k=0;k<3;k++) {
    for(i=0;i<r;i++) {
        for(j=0;j<c;j++) {
            scanf("%d%d",&a[k][i][j]);
        }
    }
}

Let's make use of a 3-D array in Program 3.7.

![](bbox=[0.115, 0.535, 0.635, 0.875])