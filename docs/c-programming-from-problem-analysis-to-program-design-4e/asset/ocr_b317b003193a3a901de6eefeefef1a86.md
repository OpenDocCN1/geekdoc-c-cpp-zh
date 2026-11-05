# CONSTANTS

Because this application is not interactive, which means it does not allow the user to input values, decisions have to be made about what data will not change. The number of inches in a foot never changes; the number of square feet in a square yard never changes. Both of these items are defined as constants. The names of the different types of carpet by category are also defined as constants. Notice in Table 2-19 that all uppercase characters are used as identifiers for constants to delineate the constants clearly from the variables. For readability, the underscore character is used as a separator between words.

The actual prices of the different carpets could be defined as constants. Constant definitions are normally placed at the top of the program to make it easy to locate and modify their values when changes are necessary. Instead of declaring the prices as constants, numeric literals are used to initialize the variable’s values. After you learn how to enter values interactively as your program is running, you might want to revise your solution so that the price can be inputted by the user. For now, the 27.95 and 15.95 are used as numeric literals for the price.

# TABLE 2-19  Constants

| Data item description | Type | Identifier | Value |
|---|---|---|---|
| Number of square feet in one square yard | `int` | `SQ_FT_PER_SQ_YARD` | 9 |
| Number of inches in one foot | `int` | `INCHES_PER_FOOT` | 12 |
| String of characters representing the best carpet name | `string` | `BEST_CARPET` | "Berber" |
| String of characters representing economy carpet name | `string` | `ECONOMY_CARPET` | "Pile" |