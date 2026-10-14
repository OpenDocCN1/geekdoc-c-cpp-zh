```
int outcome = 0;
// TODO: Multiply lhs by rhs and store the result in outcome
outcome = lhs * rhs;
expression.Text = $"{lhsOperand.Text} * {rhsOperand.Text}";
result.Text = outcome.ToString();
}

private void divideValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: Divide lhs by rhs and store the result in outcome
    outcome = lhs / rhs;
    expression.Text = $"{lhsOperand.Text} / {rhsOperand.Text}";
    result.Text = outcome.ToString();
}

private void remainderValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: Work out the remainder after dividing lhs by rhs and store the result in outcome
    outcome = lhs % rhs;
    expression.Text = $"{lhsOperand.Text} % {rhsOperand.Text}";
    result.Text = outcome.ToString();
}
```

# Test the MathsOperators application

+   1. On the Debug menu, click Start Debugging to build and run the application.
+   2. Type 54 in the Left Operand box, type 13 in the Right Operand box, click the + Addition option, and then click Calculate.
+   The value 67 should appear in the Result box.
+   3. Click the – Subtraction option, and then click Calculate. Verify that the result is now 41.
+   4. Click the * Multiplication option, and then click Calculate. Verify that the result is now 702.
+   5. Click the / Division option, and then click Calculate. Verify that the result is now 4.
+   In real life, 54/13 is 4.153846 recurring, but this is not real life—this is C# performing integer division. When you divide one integer by another integer, the answer you get back is an integer, as explained earlier.
+   6. Click the % Remainder option, and then click Calculate. Verify that the result is now 2.
+   When dealing with integers, the remainder after dividing 54 by 13 is 2; (54