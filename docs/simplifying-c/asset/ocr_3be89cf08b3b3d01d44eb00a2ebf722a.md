Note the statement rewind(fp_item) in Program 8. The function rewind is used to set the file pointer at the beginning of the file. When the first iteration is performed and the user enters 5, the file pointer is positioned at 28*4 bytes forward in the file. Now, if the user wishes to continue to search, the file pointer needs to be repositioned to the beginning of the file. The rewind(fp_item) statement rewinds and positions the file pointer fp_item to the beginning of file itemb.

# Locating the File Pointer Position

The function ftell is used to know the position in a file at which its corresponding file pointer is pointing. It returns this position as a long int. which is an offset from the beginning of the file. The syntax of the function ftell is as follows:

```
n=ftell(file_pointer);
```

The function ftell accepts one parameter. The parameter is the file pointer, which is pointing to the file to be accessed. Program 9 illustrates the use of function ftell:

# ▶ Program 9

```
/* Program to illustrate the use of function ftell */
#include<stdio.h>
#define TRUE 1
#define FALSE 0
/* Beginning of main function */
main()
{
FILE *fp_item;
struct item
{
int i_itemno;
char c_itemname[20];
int i_itemqty;
float f_itemrate;
}items;
int i_resize=sizeof(items);
int i_ctr=0,i_num,found;
char c_temp,c_ans,c_item[20];

fp_item=fopen("itemb","rb");
if (fp_item==NULL)
printf("Error in opening a file\n");
else
{
do
{
printf("\n Enter Name of item: ");
scanf("%s",&c_item);
rewind(fp_item);
found=FALSE;
while (fread(&items,i_resize,1,fp_item)!=NULL)
{
if (strcmp(c_item,items.c_itemname)==0)
```