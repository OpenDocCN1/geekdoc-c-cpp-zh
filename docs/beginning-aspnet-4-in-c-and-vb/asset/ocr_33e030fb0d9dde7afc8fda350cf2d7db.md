```
private DataView AttendeeData
{
    get
    {
        return MRBData.Tables["Attendees"].DefaultView;
    }
}

private DataView EventDetailData
{
    get
    {
        if (EventList != null && EventList.SelectedValue != null)
        {
            return new DataView(MRBData.Tables["Events"], "ID=" +
                EventList.SelectedValue.ToString(), "",
                DataViewRowState.CurrentRows);
        }
        else
        {
            return null;
        }
    }
}
```

You can also remove the existing EventData field and EventData property.

Most of these properties are simple; it's only the last that does anything new. In this case, you are filtering the data in the Events table to obtain just one event — ready to display in the detail view FormView control.

Now that you aren't using data source controls, you have to bind data yourself. A call to the DataBind() method of the page will achieve this, but you also need to set the data source DataView properties for the various data-bound controls on the page. One good way to do this is to do it during an override of the OnDataBinding() event handler, as follows:

```
protected override void OnDataBinding(EventArgs e)
{
    roomList.DataSource = RoomData;
    attendeeList.DataSource = AttendeeData;
    EventList.DataSource = EventData;
    FormView1.DataSource = EventDetailData;
    base.OnDataBinding(e);
}
```

Here you are setting the DataSource properties of roomList, attendeeList, EventList, and FormView1 to the properties defined earlier. Next, you can add the DataBind() call to Page_Load():

```
void Page_Load(object sender, EventArgs e)
{
    if (!this.IsPostBack)
    {
        nameBox.Text = Context.User.Identity.Name;
        DateTime trialDate = DateTime.Now;
        calendar.SelectedDate = GetFreeDate(trialDate);
        DataBind();
    }
}
```

Also, you must change submitButton_Click() to use the web service AddData() method. Again, much of the code can remain unchanged; only the data addition code needs changing:

```
void submitButton_Click(object sender, EventArgs e)
{
    if (Page.IsValid)
    {
        ...
```