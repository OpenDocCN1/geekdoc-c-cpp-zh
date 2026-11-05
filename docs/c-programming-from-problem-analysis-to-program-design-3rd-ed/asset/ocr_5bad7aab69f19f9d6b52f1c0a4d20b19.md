```
```csharp
//
// ckBoxWater
//
this.ckBoxWater.Location = new
    System.Drawing.Point(69, 210);
this.ckBoxWater.Name = "ckBoxWater";
this.ckBoxWater.Size = new System.Drawing.Size(64, 24);
this.ckBoxWater.TabIndex = 6;
this.ckBoxWater.Text = "Water";
this.ckBoxWater.CheckedChanged += new
    System.EventHandler(this.ckBoxWater_CheckedChanged);

//
// menuStrip1
//
this.menuStrip1.Items.AddRange(new
    System.Windows.Forms.ToolStripItem[] {
        this.fileToolStripMenuItem,
        this.editToolStripMenuItem,
        this.helpToolStripMenuItem });
this.menuStrip1.Location = new
    System.Drawing.Point(0, 0);
this.menuStrip1.Name = "menuStrip1";
this.menuStrip1.Size = new
    System.Drawing.Size(342, 24);
this.menuStrip1.TabIndex = 7;
this.menuStrip1.Text = "menuStrip1";

//
// fileToolStripMenuItem
//
this.fileToolStripMenuItem.DropDownItems.AddRange(new
    System.Windows.Forms.ToolStripItem[] {
        this.menuPlaceOrder,
        this.menuClearOrder,
        this.menuDisplayOrder,
        this.menuExit});
this.fileToolStripMenuItem.Name =
    "fileToolStripMenuItem";
this.fileToolStripMenuItem.Size = new
    System.Drawing.Size(35, 20);
this.fileToolStripMenuItem.Text = "File";

//
// menuPlaceOrder
//
this.menuPlaceOrder.Name = "menuPlaceOrder";
this.menuPlaceOrder.Size = new
    System.Drawing.Size(152, 22);
this.menuPlaceOrder.Text = "Place Order";
```
```