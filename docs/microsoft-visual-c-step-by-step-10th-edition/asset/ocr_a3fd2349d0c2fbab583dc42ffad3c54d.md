```
private void multiplyValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: Multiply lhs by rhs and store the result in outcome
    outcome = lhs + rhs;
    expression.Text = `$`${lhsOperand.Text} * ${rhsOperand.Text}``;
    result.Text = outcome.ToString();
}
private void divideValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: Divide lhs by rhs and store the result in outcome
    outcome = lhs / rhs;
    expression.Text = `$`${lhsOperand.Text} / ${rhsOperand.Text}``;
    result.Text = outcome.ToString();
}
private void remainderValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: Calculate the remainder after dividing lhs by rhs and store the result in outcome
    outcome = lhs % rhs;
    expression.Text = `$`${lhsOperand.Text} % ${rhsOperand.Text}``;
    result.Text = outcome.ToString();
}
```