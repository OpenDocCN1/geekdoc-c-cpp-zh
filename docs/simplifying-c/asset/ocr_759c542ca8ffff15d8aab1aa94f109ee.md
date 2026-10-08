```
char c_itemname[20], c_item, c_ans;
int i_itemqty, i_ctr = 0;
float f_itemrate, f_amount = 0;

fp_item = fopen("item", "w");  /* Opening a file for writing */
if (fp_item == NULL)
{
    printf("Error in opening a file\n");
    exit(1);
}
else
{
    do
    {
        i_ctr = i_ctr + 1;
        printf("\n Enter record number %d: ", i_ctr);
        printf("\n Enter item name, item rate and item quantity: ");
        scanf("%s %f %d", c_itemname, &f_itemrate, &i_itemqty);
        c_temp = getchar();
        /* writing into file */

        fprintf(fp_item, "%s %f\n", c_itemname, f_itemrate, i_itemqty);
        printf("\nWould like to add another record yes(y)/No(n): ");
        scanf("%c", &c_ans);
    } while ((c_ans == 'y') || (c_ans == 'Y'));
    fclose(fp_item);
}

fp_item = fopen("item", "r");

if (fp_item == NULL)
{
    printf("Error in opening a file\n");
    exit(1);
}
else
{
    printf("\nThe records entered in file are:\n\n");
    while ((fscanf(fp_item, "%s %f %d", c_itemname, &f_itemrate, &i_itemqty)) != EOF)
    {
        printf("%-10s %5.2f\n", c_itemname, f_itemrate, i_itemqty);
        printf("\n\n");
        f_amount = f_amount + f_itemrate * i_itemqty;
    }
    printf("Total amount to be paid is %.2f Rs.\n", f_amount);
}
fclose(fp_item);
return;

/* End of function main */
```