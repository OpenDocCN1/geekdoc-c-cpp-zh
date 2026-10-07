```
{
    int command = 0;
    command = menu();
    while (command != 5 ) {
        /* Get user's selection and branch based on the input. */
        switch (command) {
            case 1: {
                puts("\nExecuting task A.");
                delay();
                break;
            }
            case 2: {
                puts("\nExecuting task B.");
                delay();
                break;
            }
            case 3: {
                puts("\nExecuting task C.");
                delay();
                break;
            }
            case 4: {
                puts("\nExecuting task D.");
                delay();
                break;
            }
            case 5: {
                /* Exit program. */
                puts("\nExiting program...\n");
            }
            default: {
                puts("\nInvalid choice, try again.");
            }
        } /* End of switch */
        command = menu();
    }
    return 0;
}
/* Displays a menu and inputs user's selection. */
int menu(void)
```