
## PROGRAM 2

Write a C# program to print Fibonacci series without using recursion and using recursion.

```
using System;

public class FibonacciExample
{
    public static void Main(string[] args)
    {
        int n1=0,n2=1,n3,i,number;
        Console.Write("Enter the number of elements: ");
        number = int.Parse(Console.ReadLine());
        Console.Write(n1+" "+n2+" "); //printing 0 and 1
        for(i=2;i<number;++i) //loop starts from 2 because 0 and 1 are already printed
        {
            n3=n1+n2;
            Console.Write(n3+" ");
            n1=n2;
            n2=n3;
        }
    }
}
```

### Output

Enter the number of elements: 15

0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

## PROGRAM 3

Write a C# program to print factorial of a number.

```
using System;

public class FactorialExample
{
    public static void Main(string[] args)
    {
        int i,fact=1,number;
        Console.Write("Enter any Number: ");
        number = int.Parse(Console.ReadLine());
        for(i=1;i<=number;i++){
            fact=fact*i;
        }
        Console.Write("Factorial of "+number+" is: "+fact);
    }
}
```

### Output

Enter any Number: 6

Factorial of 6 is: 720

## PROGRAM 4

Write a C# program to print alphabet triangle.

```
using System;

public class PrintExample
{
    public static void Main(string[] args)
    {
        char ch='A';
        int i, j, k, m;

        for(i=1; i<=5; i++)
        {
            for(j=5; j>=i; j--)
                Console.Write(" ");

            for(k=1; k<=i; k++)
                Console.Write(ch++);

            ch--;

            for(m=1; m<i; m++)
                Console.Write(--ch);

            Console.Write("\n");
            ch='A';
        }
    }
}
```

### Output

A

ABA

ABCBA

ABCDCBA

ABCDEDCBA

## PROGRAM 5

Write a VB.NET program to design following screen, accept the details from the user. Clicking on Submit button Net Salary should be calculated and displayed into the textbox. Display the messagebox informing the Name and Net Salary of employee.

![](img/e7ca4af023a4148a909dd82c11f81893_288_0.png)

### Program

```
Public Class Slip7

    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click

        Dim cal, tax, bs, da, hra, ma, pf, pt, it As Integer

        bs = CInt(TextBox2.Text)
        da = CInt(TextBox3.Text)
        hra = CInt(TextBox4.Text)
        ma = CInt(TextBox5.Text)
        pf = CInt(TextBox6.Text)
        pt = CInt(TextBox7.Text)
        it = CInt(TextBox8.Text)

        cal = bs + ((da * bs) / 100) + ((hra * bs) / 100) + ((ma * bs) / 100)
        tax = ((pt * bs) / 100) + ((it * bs) / 100) + ((pf * bs) / 100)
        cal = cal - tax

        TextBox9.Text = cal

        MsgBox("Name: " + TextBox1.Text + " Net salary: " + TextBox9.Text)

    End Sub

End Class
```

### Output

![](img/e7ca4af023a4148a909dd82c11f81893_290_0.png)

## PROGRAM 6

Write a VB.NET program to design the following form, select the question number from combo box that question will be displayed into textbox and the options for that question will be displayed on four radio buttons, select option and click on submit button result should be displayed in another textbox.

![](img/e7ca4af023a4148a909dd82c11f81893_291_0.png)

### Program

```
Public Class Slip14

    Private Sub Slip14_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        ComboBox1.Items.Add("Question1")
        ComboBox1.Items.Add("Question2")
        ComboBox1.Items.Add("Question3")
    End Sub

    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        If ComboBox1.SelectedItem() = "Question1" Then
            If RadioButton1.Checked = True Then
                TextBox2.Text = "Answer is Correct."
            Else
                TextBox2.Text = "Answer is Wrong."
            End If
        End If

        If ComboBox1.SelectedItem() = "Question2" Then
            If RadioButton2.Checked = True Then
                TextBox2.Text = "Answer is Correct."
            Else
                TextBox2.Text = "Answer is Wrong."
            End If
        End If

        If ComboBox1.SelectedItem() = "Question3" Then
            If RadioButton4.Checked = True Then
                TextBox2.Text = "Answer is Correct."
            Else
                TextBox2.Text = "Answer is Wrong."
            End If
        End If
    End Sub

    Private Sub ComboBox1_SelectedIndexChanged(sender As Object, e As EventArgs) Handles ComboBox1.SelectedIndexChanged
        RadioButton1.Visible = True
        RadioButton2.Visible = True
        RadioButton3.Visible = True
        RadioButton4.Visible = True

        If ComboBox1.SelectedItem() = "Question1" Then
            TextBox1.Text = "What is capital of India?"
            TextBox2.Text = ""
            RadioButton1.Checked = False
            RadioButton2.Checked = False
            RadioButton3.Checked = False
            RadioButton4.Checked = False
            RadioButton1.Text = "New Delhi"
            RadioButton2.Text = "Mumbai"
            RadioButton3.Text = "Pune"
            RadioButton4.Text = "Chennai"
        ElseIf ComboBox1.SelectedItem() = "Question2" Then
            TextBox1.Text = "What is Capital of USA?"
            TextBox2.Text = ""
            RadioButton1.Checked = False
            RadioButton2.Checked = False
            RadioButton3.Checked = False
            RadioButton4.Checked = False
            RadioButton1.Text = "New York"
            RadioButton2.Text = "Washington DC"
            RadioButton3.Text = "California"
            RadioButton4.Text = "Georgia"
        ElseIf ComboBox1.SelectedItem() = "Question3" Then
            TextBox1.Text = "What is capital of Germany?"
            TextBox2.Text = ""
            RadioButton1.Checked = False
            RadioButton2.Checked = False
            RadioButton3.Checked = False
            RadioButton4.Checked = False
            RadioButton1.Text = "Frankfurt"
            RadioButton2.Text = "Washington DC"
            RadioButton3.Text = "Hamburg"
            RadioButton4.Text = "Berlin"
        End If
    End Sub

End Class
```

### Output

![](img/e7ca4af023a4148a909dd82c11f81893_296_0.png)

## PROGRAM 7

Write a VB.NET program to design the following form, this program shows the details of students in the form of a form (use SplitContainer or GroupBox control to separate the input and output session).

![](img/e7ca4af023a4148a909dd82c11f81893_297_0.png)

### Program

```
Public Class Slip17

    Private Sub Slip17_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        ComboBox1.Items.Add("BCA")
        ComboBox1.Items.Add("BSC")
        ComboBox1.Items.Add("MCA")
        SplitContainer1.Panel2.Hide()
    End Sub

    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        SplitContainer1.Panel2.Show()
        Label26.Text = TextBox1.Text
        Label25.Text = TextBox2.Text
        Label24.Text = TextBox3.Text
        Label23.Text = ComboBox1.SelectedItem()

        If RadioButton1.Checked = True Then
            Label22.Text = RadioButton1.Text
        ElseIf RadioButton2.Checked = True Then
            Label22.Text = RadioButton2.Text
        End If

        Label21.Text = DateTimePicker1.Value
        Label20.Text = TextBox4.Text
        Label19.Text = TextBox5.Text
    End Sub

End Class
```

### Output

### Student Information

Student's Name ABC  
Father's Name DEF  
Mother's Name GHI  
Course BCA  
Gender Female  
Date of Birth Tuesday July  
Hobbies JKL  
Contact Number 1234567890

### Display Student Information

Student's Name: ABC  
Father's Name: DEF  
Mother's Name: GHI  
Course: BCA  
Gender: Female  
Date of Birth: 7/1/2003 9:22:14 PM  
Hobbies: JKL  
Contact Number: 1234567890

## PROGRAM 8

Write a VB.NET program to design the following form, accept all details from user and display the details through message box.

![](img/e7ca4af023a4148a909dd82c11f81893_300_0.png)

### Program

```
Public Class Slip18

    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click

        Dim a, b As String

        If CheckBox1.Checked = True Then
            a = CheckBox1.Text
        ElseIf CheckBox2.Checked = True Then
            a = CheckBox2.Text
        ElseIf CheckBox3.Checked = True Then
            a = CheckBox3.Text
        End If

        If RadioButton1.Checked = True Then
            b = RadioButton1.Text
        ElseIf RadioButton2.Checked = True Then
            b = RadioButton2.Text
        ElseIf RadioButton3.Checked = True Then
            b = RadioButton3.Text
        End If

        MsgBox("Name : " + TextBox1.Text + " Qualification : " + a + " post: " + b)

    End Sub

End Class
```

## PROGRAM 9

### Students Marksheet Result Program in VB.NET

Create one class student which stores information of student's Roll no, Name, Total marks, which cannot be used from outside the class. Student class must provide proper methods to read and write this information. The child class must provide function for calculating the total which should be stored in Total Marks of base class. The child classes must have the correct method for calculating percentage according to no. of subjects. Demonstrate the use of these classes.

FYBCA.VB

```
Public Class FYBCA

    Inherits student

    Dim i As Integer = 0

    Dim submark(4) As Integer

    Public Property calculatemark As Integer

        Set(ByVal value As Integer)

            submark(i) = value

            i += 1

        End Set
```
