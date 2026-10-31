```
_mdl.Render();
}

private void WebForm1_PreRender(object sender, System.EventArgs e)
{
    srcpnl.Controls.Clear();
    stashpnl.Controls.Clear();
    MdlRender();
}
```

The srcpnl, the candy source panel, and stashpnl, the candy stash panel, are Panels (the control in the WebControls namespace) I've added with the form designer in Visual Studio.

Of course, the form implements PickCandyView. The code is fairly simple. Any decisions made (if statements) concern appearance only, not the state of the interaction. This is crucial. The model must be responsible for the latter.

```
void PickCandyView.SourceItem(string text, bool pickable)
{
    int index = _srcTbl.Rows.Count;
    HtmlTableRow tr = AddTR(_srcTbl);
    HtmlTableCell td = AddTD(tr);
    td.InnerText = text;

    td = AddTD(tr);
    if (pickable)
    {
        LinkButton lb = new LinkButton();
        td.Controls.Add(lb);
        lb.ID = "pick" + index.ToString();
        lb.Text = ">>";
        lb.Click += new EventHandler(Pick_Click);
    }
}
```

```
void PickCandyView.StashItem(string text)
{
    AddTD(AddTR(_stashTbl)).InnerText = text;
}
```

And finally, here's the pick callback method:

```
private void Pick_Click(object sender, EventArgs e)
{
    _mdl.PickAt(IndexFromID(sender));
}
```

Yes, I trust you to read between the lines. The only possibly non-trivial thing I left for you to figure out is the CreateRetriever() method. You've seen something similar to what's needed in the test