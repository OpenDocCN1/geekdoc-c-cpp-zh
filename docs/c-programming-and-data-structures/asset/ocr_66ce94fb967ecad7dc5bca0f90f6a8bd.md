```
{
    case 1:
        perks = CA1 + EA1;
        break;
    case 2:
        perks = CA2 + EA2;
        break;
    case 3:
        perks = CA3 + EA3;
        break;
    case 4:
        perks = CA4 + EA4;
        break;
    default:
        printf("Error in level code\n");
        goto stop;
}
house_rent = 0.25 * basic;
gross = basic + house_rent + perks;
if (gross <= 2000)
    incometax = 0;
else if (gross <= 4000)
    incometax = 0.03 * gross;
else if (gross <= 5000)
    incometax = 0.05 * gross;
else
    incometax = 0.08 * gross;
net = gross - incometax;
printf("%d %d %.2f\n", level, jobnumber, net);
goto input;
stop: printf("\n\nEND OF THE PROGRAM");
}
```

# Output

Enter level, job number, and basic pay
Enter 0 (zero) for level to END
1 1111 4000
1 1111 5980.00
Enter level, job number, and basic pay
Enter 0 (zero) for level to END
2 2222 3000
2 2222 4465.00
Enter level, job number, and basic pay
Enter 0 (zero) for level to END
3 3333 2000
3 3333 3007.00
Enter level, job number, and basic pay
Enter 0 (zero) for level to END
4 4444 1000
4 4444 1500.00
Enter level, job number, and basic pay
Enter 0 (zero) for level to END
0
END OF THE PROGRAM