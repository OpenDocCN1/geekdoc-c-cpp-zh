# Program:-

```
Public Class slip7

Private Sub Button1_Click(sender As Object, e As eventargs) Handles Button1.Click

    Dim cal, tax, bs, da, hra, ma, pf, pt, it As Integer

    Bs = cint(textbox2.Text)

    Da = cint(textbox3.Text)

    Hra = cint(textbox4.Text)

    Ma = cint(textbox5.Text)

    Pf = cint(textbox6.Text)

    Pt = cint(textbox7.Text)

    It = cint(textbox8.Text)

    Cal = bs + ((da * bs) / 100) + ((hra * bs) / 100) + ((ma * bs) / 100)

    Tax = ((pt * bs) / 100) + ((it * bs) / 100) + ((pf * bs) / 100)

    Cal = cal - tax

    Textbox9.Text = cal

    Msgbox("Name: " + textbox1.Text + " Net salary: " + textbox9.Text)
```