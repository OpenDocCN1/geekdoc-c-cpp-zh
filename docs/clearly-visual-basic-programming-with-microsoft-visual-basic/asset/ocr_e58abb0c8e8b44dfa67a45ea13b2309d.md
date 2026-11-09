and commission rate, a button to calculate and display the annual commission, and a label to show the annual commission to the user. In addition to the controls required by the algorithm, every interface also needs a control that allows the user to end the application. In this interface, you will use a button marked Exit for this purpose. Figure 5-2 lists the controls mentioned in this section.

| Control | Purpose |
|---|---|
| Label | show the annual commission |
| Text box | get the annual sales |
| Text box | get the commission rate |
| Button (Calculate Commission) | calculate and display the annual commission |
| Button (Exit) | end the application |

Figure 5-2: Listing of controls

You should assign a meaningful name to each of the controls listed in Figure 5-2, because doing so will help you keep track of the various objects included in the interface. In addition, as you will learn in Chapter 6, the programmer uses an object’s name to refer to the object in code. The name must begin with a letter and can contain only letters, numbers, and the underscore character. You cannot include punctuation characters or spaces in the name. There are several conventions for naming objects in Visual Basic; in this book, you will use a naming convention called Hungarian notation. Names in Hungarian notation begin with a three (or more) character ID that represents the object’s type. Label control names, for example, begin with lbl. Names of buttons begin with btn, and text box names begin with txt. The remaining characters in the name represent the object’s purpose. For instance, using Hungarian notation, you might assign the name lblCommission to the label that displays the annual commission. The “lbl” identifies the object as a label, and “Commission” reminds you of the label’s purpose. Hungarian notation names are entered using **camel case**, which means you lowercase the ID characters and then uppercase the first letter of each word in the name. Camel case refers to the fact that the uppercase letters appear as “humps” in the name because they are taller than the lowercase letters. Figure 5-3 lists the name and purpose of each of the controls listed in Figure 5-2.

| Control name | Purpose |
|---|---|
| lblCommission | show the annual commission |
| txtSales | get the annual sales |
| txtRate | get the commission rate |
| btnCalculate (Calculate Commission) | calculate and display the annual commission |
| btnExit (Exit) | end the application |

Figure 5-3: Name and purpose of each control