
## An UpdateProgress control in Design view

![](img/c024ccf88e28c30c07dd410d4342288f_734_0.png)

### Three attributes of the UpdateProgress control

| Attribute | Description |
|---|---|
| DynamicLayout | Determines whether space is allocated on the page for the content of the control when it isn’t displayed. The default is True, which means that space is dynamically allocated. If set to False, space is allocated for the content even though it won’t be seen until an asynchronous postback occurs. |
| DisplayAfter | Determines how long, in milliseconds, after the asynchronous postback has started to display the content. The default is 500 milliseconds (0.5 seconds). This value can prevent the content from flickering when the postback happens quickly. |
| AssociatedUpdatePanelID | The ID of the UpdatePanel control that the control is associated with. |

### The aspx code for an UpdatePanel control with an UpdateProgress control

```aspx
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
    <ContentTemplate>
        <asp:UpdateProgress ID="UpdateProgress1" runat="server">
            <ProgressTemplate>
                Please wait. The update is in progress.
            </ProgressTemplate>
        </asp:UpdateProgress>
    </ContentTemplate>
</asp:UpdatePanel>
```

### Description

- An UpdateProgress control must contain a ProgressTemplate element that defines the content of the control. This content is displayed only while an asynchronous postback is in progress. It is hidden after the asynchronous postback is complete.

Figure 21-10   How to use the UpdateProgress control

## An application that uses AJAX

To illustrate how an application that uses AJAX works, the topics that follow present an application that uses a shout box. A shout box can be used to implement an informal comment system on a web site. Unlike traditional comment systems, users aren’t required to register to enter shouts and shouts are typically displayed only for a short period of time. By AJAX-enabling this shout box, it can be updated without interfering with what the user is doing.

## The Shout Box application

Figure 21-11 presents the Shout Box application. To start, this application lets the user display the products in a selected category in a DataList control. This part of the web page is not AJAX-enabled and works just like the Product List application you saw in chapter 13.

To the right of the DataList control are the controls that are used to implement the shout box. These controls are placed inside two UpdatePanel controls. The first update panel includes a label that displays the shout box, along with a Timer control that causes the shout box to be updated every five seconds. The second update panel includes two text boxes that let the user enter the information for a shout, labels that identify the text boxes, required field validators for the text boxes, a button that submits the shout, and an UpdateProgress control.

Notice that the shouts in the shout box are displayed in reverse chronological order. In other words, they’re displayed from the newest shout to the oldest shout. That way, if there are many shouts being displayed, the user won’t have to scroll down to see the newest ones.

The shouts for this application are displayed in the shout box for three minutes. The shouts that are currently displayed are stored in a list in application state. That makes sense since the shouts are temporary. If you wanted to have a permanent record of the shouts, however, you could store them in a database and then display just the most recent shouts in the shout box.

![](img/c024ccf88e28c30c07dd410d4342288f_736_0.png)

### Description

- The Shout Box application is a variation of the Product List application you saw in chapter 13. It lets users post short messages, called shouts, which are then displayed in a shout box for other users to see.
- A list of the shout items that are currently displayed is stored in an application state variable. Shout items that are over three minutes old are deleted from this list whenever the shout box is updated or displayed.
- To implement the shout box, this page uses two UpdatePanel controls. The first one contains a label that’s used to display the shout items and a Timer control that updates the panel every five seconds. The second one contains the controls that are used to submit a shout and display a progress indicator. It also contains required field validators for the two text boxes.

Figure 21-11   The Shout Box application

### The ShoutItem class

Each shout that’s displayed in the shout box for this application is created from the ShoutItem class shown in figure 21-12. As you can see, this class includes three properties named UserName, Timestamp, and Comment.

### The ShoutItemList class

The ShoutItemList class, also shown in figure 21-12, is a bit more complicated. This class starts by declaring a private field named shoutList that stores the list of ShoutItem objects that are displayed in the shout box. Then, it includes three methods that are used to display items in the shout box and keep the list of items in the shout box current.

The first method, Purge, is a private method that examines the shouts in the shoutList variable and removes any that are too old. It starts by setting a variable named purgeTime to the current time and then subtracting three minutes. This variable is used to determine how long the shouts are displayed.

Next, the Purge method uses a while statement to determine if any of the items in the shout list are older than three minutes. The condition on this statement causes the loop to be executed for each item in the shoutList variable. Although you might think you could use a foreach statement here, you can’t. That’s because the shout list is being updated as the loop executes. To make this work, then, you have to use a while loop with an index variable to manually keep track of the current position in the shout list.

Within the while loop, the Timestamp property of the current shout item is compared with the purgeTime variable. Then, if the timestamp is less than or equal to the purge time, the shout item is removed from the shout list. In that case, the index isn’t updated because the shout items that come after the one that was removed are moved up in the list. If the shout item isn’t removed from the list, however, the index variable is increased by one so the next item can be checked.

The public Add method adds the shout item that’s passed to it to the beginning of the shout list. But first, it calls the Purge method to remove any old shout items. In addition, it executes the Sleep method of the current thread to delay the Add method by two seconds. I included this method to ensure that the UpdateProgress control is displayed. Of course, you wouldn’t want to include code like this in a production application.

The public Display method returns a text string that contains the contents of the shout box. Like the Add method, it starts by calling the Purge method. Then, it creates a StringBuilder object that will store the shout box text.

If the shout list contains at least one item, the Display method continues by adding a <dl> tag to the StringBuilder object. This tag defines a definition list, which can contain a formatted list of text items. Then, it uses a foreach loop to add the information for each shout item to this list. In this case, the user name

### The ShoutItem.cs file

```
using System;

public class ShoutItem
{
    public string UserName { get; set; };
    public DateTime Timestamp { get; set; };
    public string Comment { get; set; };
}
```

### The ShoutItemList.cs file

```
using System;
using System.Collections.Generic;
using System.Text;

public class ShoutItemList
{
    private List<ShoutItem> shoutList = new List<ShoutItem>();

    private void Purge() {
        DateTime purgeTime = DateTime.Now;
        purgeTime = purgeTime.AddMinutes(-3);
        int i = 0;
        while (i < shoutList.Count)
        {
            if (shoutList[i].Timestamp <= purgeTime)
                shoutList.RemoveAt(i);
            else
                i += 1;
        }
    }

    public void Add(ShoutItem shout) {
        Purge();
        System.Threading.Thread.Sleep(2000);
        shoutList.Insert(0, shout);
    }

    public string Display() {
        Purge();
        StringBuilder shoutBoxText = new StringBuilder();
        if (shoutList.Count > 0)
        {
            shoutBoxText.AppendLine("<dl>");
            foreach (ShoutItem shout in shoutList)
            {
                shoutBoxText.Append("<dt>" + shout.UserName + " (");
                shoutBoxText.Append(shout.Timestamp.ToShortTimeString() + ")");
                shoutBoxText.Append("</dt>");
                shoutBoxText.AppendLine("<dd>" + shout.Comment + "</dd>");
            }
            shoutBoxText.AppendLine("</dl>");
        }
        return shoutBoxText.ToString();
    }
}
