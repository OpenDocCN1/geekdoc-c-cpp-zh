# Controlling Output to the Screen

28: puts("nuse * field width specifier to obtain field width");

29: puts("from a variable in the argument list.\n");

30:

31: for (n=5;n<=25; n+=5);

32: printf("*f\n", n, d1);

33:

34: puts("\n Press Enter to continue...");

35: fflush(stdin);

36: getchar();

37:

38: puts("\nInclude leading zeros.\n");

39:

40: printf("%05f\n", d1);

41: printf("%010f\n", d1);

42: printf("%015f\n", d1);

43: printf("%020f\n", d1);

44: printf("%025f\n", d1);

45:

46: puts("\n Press Enter to continue...");

47: fflush(stdin);

48: getchar();

49:

50: puts("\nDisplay in octal, decimal, and hexadecimal.");

51: puts("Use # to precede octal and hex output with 0 and 0X.");

52: puts("Use - to left-justify each value in its field.")");"

53: puts("First display column labels.\n");

54:

55: printf("%-15s%-15s%-15s, m2, m3, m4");

56:

57: for (n=1;n<20; n++)

58: printf("%-15d-%#15d-%#15X, n, n, n");

59:

60: puts("\n Press Enter to continue...");

61: fflush(stdin);

62: getchar();

63:

64: puts("\nuse the tn conversion command to count characters.\n");

65:

66: printf("%s%s%s%s\n", m1, m2, m3, m4, &n);

67:

68: printf("\n\nThe last printf() output d characters.\n", n);

69:

70: return 0;

71: }

# **Output**

Outputting a number with different field widths.

10000.123047