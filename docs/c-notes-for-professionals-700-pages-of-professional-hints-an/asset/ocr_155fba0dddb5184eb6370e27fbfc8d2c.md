Quote from It's All About the SynchronizationContext.

# Section 115.3: Why SynchronizationContext is so important?

Consider this example:

```
private void button1_Click(object sender, EventArgs e)
{
    label1.Text = RunTooLong();
}
```

This method will freeze UI application until the RunTooLong will be completed. The application will be unresponsive.

You can try run inner code asynchronously:

```
private void button1_Click(object sender, EventArgs e)
{
    Task.Run(() => label1.Text = RunTooLong());
}
```

But this code won't execute because inner body may be run on non-UI thread and it shouldn't change UI properties directly:

```
private void button1_Click(object sender, EventArgs e)
{
    Task.Run(() =>
    {
        var label1Text = RunTooLong();

        if (label1.InvokeRequired)
            label1.BeginInvoke((Action) delegate() { label1.Text = label1Text; });
        else
            label1.Text = label1Text;
    });
}
```

Now don't forget always to use this pattern. Or, try SynchronizationContext.Post that will make it for you:

```
private void button1_Click(object sender, EventArgs e)
{
    Task.Run(() =>
    {
        var label1Text = RunTooLong();
        SynchronizationContext.Current.Post((obj) =>
        {
            label1.Text = label1Text;
        }, null);
    });
}
```