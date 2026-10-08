```
{
            i_num = ftell(fp_item) / i_recsize;
            found = TRUE;
            break;
        }
    }
    if (!found)
        printf("\nThe record you are searching is not\n\n");
    else
    {
        printf("\n The record is available at %d\n");
        printf("position", i_num);
        printf("\nThe record details are.........\n");
        printf("%d %s %f %d", items.c_itemno, items.c_itemname, items.f_itemrate, items.i_itemqty);
    }
    c_temp = getchar();
    printf("\nDo you want to continue: ");
    scanf("%c", &c_ans);
} while (c_ans == 'y' || c_ans == 'Y');
    fclose(fp_item);
    return;
}
    /* End of function main */
```

**Output:**

Enter Name of item: Pen

The record is available at 1 position

The record details are.........

1 Pen 10.000000 12

Do you want to continue: y

Enter Name of item: Pencil

The record is available at 2 position

The record details are.........

2 Pencil 1.500000 50

Do you want to continue: y

Enter Name of item: Eraser

The record you are searching is not available!!!

Do you want to continue: n

Program 9 accepts the name of the item from the user. It then reads the record of the file itemb one by one. The read record contains item name. This item name is compared with