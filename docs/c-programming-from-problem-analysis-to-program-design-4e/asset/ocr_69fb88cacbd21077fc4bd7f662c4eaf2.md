```
```csharp
this.ckBxWater.Text = "Water";
this.ckBxWater.CheckedChanged += new
    System.EventHandler(this.ckBxWater_CheckedChanged);

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

// menuPlaceOrder
//
this.menuPlaceOrder.Name = "menuPlaceOrder";
this.menuPlaceOrder.Size = new
    System.Drawing.Size(152, 22);
this.menuPlaceOrder.Text = "Place Order";
this.menuPlaceOrder.Click += new System.EventHandler
    (this.menuPlaceOrder_Click);

// menuClearOrder
//
this.menuClearOrder.Name = "menuClearOrder";
this.menuClearOrder.Size = new
    System.Drawing.Size(152, 22);
this.menuClearOrder.Text = "Clear Order";
this.menuClearOrder.Click += new System.EventHandler
    (this.menuClearOrder_Click);
```
```