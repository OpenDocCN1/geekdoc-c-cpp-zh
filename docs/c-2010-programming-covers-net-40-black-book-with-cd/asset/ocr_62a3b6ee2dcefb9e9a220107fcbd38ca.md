```
Label3.Text = "welcome " + TextBox2.Text;
}
```

3. Type the name and roll number in the text boxes and click the Welcome button. The Label control becomes visible with the text stating Welcome <UserName>, as shown in Figure 13.32:

![](bbox=[0.21, 0.126, 0.727, 0.366])

Figure 13.32: Displaying the Label Visible with a Welcome Message

# Disabling and Enabling Controls

You usually disable a control when you do not want a user to access the control. Typically, you disable controls having an auto-generated user id. Let’s learn how to disable a text box containing the roll number of a user. We disable the text box in the Click event of the Welcome button. To do so, add the highlighted code in the Click event of the Button control, as shown in Listing 13.7:

Listing 13.7: Code to Disable and Enable the Button Control

```
protected void Button1_Click(object sender, EventArgs e)
{
Label3.visible = true;
Label3.Text = "welcome " + TextBox2.Text;
TextBox1.Enabled = false;
}
```

By default, the Enabled property is set to true. Now, execute the application by pressing F5 key. The disabled text box appears grayed out, as shown in Figure 13.33:

![](bbox=[0.2, 0.628, 0.758, 0.896])

Figure 13.33: Displaying a Disabled Text Box