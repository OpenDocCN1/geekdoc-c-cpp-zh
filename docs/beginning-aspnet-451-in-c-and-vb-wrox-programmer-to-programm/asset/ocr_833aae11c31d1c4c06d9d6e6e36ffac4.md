# 118 | CHAPTER 4 WORKING WITH ASP.NET SERVER CONTROLS

2. Open the Wizard's Smart Tasks panel (click the arrow in its upper right-hand corner) and choose Add/Remove WizardSteps. In the dialog box that follows, click the Add button to insert a third wizard step, shown in Figure 4-12.

![](bbox=[0.125, 0.173, 0.565, 0.415])

FIGURE 4-12

3. Click the first WizardStep labeled Step 1 in the Members list on the left and change its Title from Step 1 to About You. Set the Title of the other two steps to Favorite Language and Ready, respectively.

4. Change the StepType of the second step (now labeled Favorite Language) to Finish, and the last step to Complete. You can leave the StepType of the first step to Auto. Click OK to close the WizardStep Collection Editor.

5. In Design, click About You in the list on the left to make it active and drag a Label and a TextBox to the right side of the Wizard. You drag them inside the gray rectangle that's in the upper-right corner of the Wizard, or the controls won't end up inside the Wizard. Set the Text property of the Label to Type your name and change the ID of the TextBox to YourName. When you're done, your Wizard looks like Figure 4-13.

![](bbox=[0.125, 0.695, 0.615, 0.815])

FIGURE 4-13

6. Click the Favorite Language item in the list on the left to make it active. Add a DropDownList to the rectangle with the gray border on the right part of the wizard step. Rename the DropDownList by setting its ID to FavoriteLanguage. Open the Smart Tasks panel of the DropDownList control and choose Edit Items. Add the three items you added in an earlier Try It: for C#, Visual Basic, and CSS, respectively. If you want, you can copy the three items