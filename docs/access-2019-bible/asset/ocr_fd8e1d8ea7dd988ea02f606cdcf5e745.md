This expression concatenates the bullet character—returned by Chr(149)—with the data in the CompanyName field.

# FIGURE 21.18

The bullet character is added to the Control Source property of the txtCompanyName text box.

![](bbox=[0.21, 0.31, 0.8, 0.66])

This particular trick only works if the character set (such as Arial) assigned to the control (Label or Text Box) includes a bullet character as the 149th ASCII character. Not all fonts accessible by Access applications include a bullet character, but popular typefaces such as Arial do tend to include this character.

The report now appears as shown in Figure 21.19 (with some summary information at the top that will be addressed later in this chapter). You can increase or decrease the number in the Spaces() function to pad the white space between the bullet and the text. Because the bullet character and CompanyName field have been concatenated together in the text box, they’ll be displayed in the same typeface. Also, adding the bullet character to the text box containing the company name guarantees that the spacing between the bullet and first character of the company name will be consistent in every record. When using proportionally spaced fonts such as Arial, it can sometimes be difficult to get precise alignment between report elements. Concatenating data in a text box eliminates spacing problems introduced by proportionally spaced characters. Note, though, that if the amount of text in the text box exceeds a single row, subsequent rows will not be indented.