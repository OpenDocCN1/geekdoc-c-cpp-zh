```
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        public int FindGreater(int number1, int number2)
        {
            int greater;
            if (number1 > number2)
            {
                greater = number1;
            }
            else
            {
                greater = number2;
            }
            return greater;
        }

        private void findGreaterButton_Click(object sender, EventArgs e)
        {
            int input1Int = Convert.ToInt32(input1.Text);
            int input2Int = Convert.ToInt32(input2.Text);
            int outputValue = FindGreater(input1Int, input2Int);
            output.Text = outputValue.ToString();
        }
    }
}
```

Code 11.9 (cont'd)

11. Build and run the project. When we enter two integers and click the Find the greater one Button, our method is called, finds and returns the value of the greater one and the program displays this value in the output TextBox as shown in Figure 11.4.

+   - We may pass as many inputs as we need to a method using commas as separators as we did in this project.
+   - Similarly, a method may return multiple values separated by commas if needed.