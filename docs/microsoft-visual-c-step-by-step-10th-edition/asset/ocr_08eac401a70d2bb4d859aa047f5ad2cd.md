```
private void addValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: Add rhs to lhs and store the result in outcome
    outcome = lhs + rhs;
    expression.Text = $\$\{lhsOperand.Text} + {rhsOperand.Text}";
    result.Text = outcome.ToString();
}
```