```
for(i_octr=0;i_octr< i_row; i_octr++)
{
    for(i_ict r=0;i_ict r< i_col; i_ict r++)
    {
        printf("%4d ",i_matri x[i_oct r][i_ict r]);
    }
    printf("\n");
}
} /* End of PrintValues function */
/* Function to multiply values of matrix */
void MultiplyMatrix()
{
    int i_ict r, i_jct r, i_kct r;
    for(i_ict r=0;i_ict r<i_ROW[0];i_ict r++)
    {
        for(i_jct r=0;i_jct r<i_COL[1];i_jct r++)
        {
            i_ResultMatrix[i_ict r][i_jct r]=0;
            for(i_kct r=0;i_kct r<i_ROW[0];i_kct r++)
            i_ResultMatrix[i_ict r][i_jct r] +=
            i_Amatrix[i_ict r][i_kct r] * i_Bmatrix[i_kct r][i_jct r];
        }
    }
} /* End of MultiplyMatrix function */
/* Beginning of main function */
main()
{
    printf("\nNumber of rows in Matrix A: ");
    scanf("%d",&i_ROW[0]);
    printf("\nNumber of columns in Matrix A: ");
    scanf("%d",&i_COL[0]);
    printf("\nNumber of rows in Matrix B: ");
    scanf("%d",&i_ROW[1]);
    printf("\nNumber of columns in Matrix B: ");
    scanf("%d",&i_COL[1]);
    if(i_COL[0] != i_ROW[1])
    {
        printf("Columns in first matrix must be equal Rows in second
matrix.\n");
        printf("Matrix Multiplication not possible\n");
        exit(1);
    }
    /* Read values in both Matrix */
    InputValues(i_Amatrix,i_ROW[0],i_COL[0]);
    InputValues(i_Bmatrix,i_ROW[1],i_COL[1]);
    /* Multiply the matrix */
    MultiplyMatrix();
    /* Print Result */
    printf("\nMatrix A\n");
```