![](bbox=[0.375, 0.077, 0.775, 0.485])

Figure 17-29

Create a new folder in the project and name it `images`. Add an image called `delete.png` into the `images` folder (see Figure 17-30).

![](bbox=[0.342, 0.588, 0.688, 0.74])

Figure 17-30

You will now use a `<div>` element to define the content of the popup that you want to display:

```
```html
<div id="divDialog" runat="server" class="dialog" style="display: none">
    <center>
        <img style="vertical-align: middle"
            src="images/delete.png" width="60" />
        Are you sure you want to delete this record?<br />
```
```