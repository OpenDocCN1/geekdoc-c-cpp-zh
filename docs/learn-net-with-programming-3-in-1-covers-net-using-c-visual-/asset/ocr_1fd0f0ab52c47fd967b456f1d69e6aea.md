```
14. {
15. }
16. Protected void Button1_Click(object sender, eventargs e)
17. {
1. 18. Message.Text = "Hello " + username.Text + "!";
2. 19. Message.Text = message.Text + "<br/> You have successuly Registered with the following details.";
3. 20. Showusername.Text = username.Text;
4. 21. Showemail.Text = emailid.Text;
22. If (radiobutton1.Checked)
23. {
24. Showgender.Text = radiobutton1.Text;
25. }
26. Else showgender.Text = radiobutton2.Text;
27. Var courses = "";
28. If (checkbox1.Checked)
29. {
30. Courses = checkbox1.Text + " ";
31. }
32. If (checkbox2.Checked)
33. {
34. Courses += checkbox2.Text + " ";
35. }
36. If (checkbox3.Checked)
37. {
38. Courses += checkbox3.Text;
```