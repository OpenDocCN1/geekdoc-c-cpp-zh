```
```csharp
// txtResult
this.txtResult.Location =
    new System.Drawing.Point(96, 216);
this.txtResult.Name = "txtResult";
this.txtResult.Size = new
    System.Drawing.Size(80, 27);
this.txtResult.TabIndex = 8;
this.txtResult.TextAlign =
    System.Windows.Forms.HorizontalAlignment.Right;

// groupBox1
this.groupBox1.Controls.AddRange
    (new System.Windows.Forms.Control[]
    {
        this.radAdvanc,
        this.radInterm,
        this.radBeginner});
this.groupBox1.ForeColor =
    System.Drawing.Color.Yellow;
this.groupBox1.Location =
    new System.Drawing.Point(208, 72);
this.groupBox1.Name = "groupBox1";
this.groupBox1.Size = new
    System.Drawing.Size(160, 120);
this.groupBox1.TabIndex = 9;
this.groupBox1.TabStop = false;
this.groupBox1.Text = "Skill Level";

// radAdvanc
this.radAdvanc.Location = new
    System.Drawing.Point(16, 88);
this.radAdvanc.Name = "radAdvanc";
this.radAdvanc.Size = new
    System.Drawing.Size(136, 24);
this.radAdvanc.TabIndex = 2;
this.radAdvanc.Text = "Advanced";
this.radAdvanc.Click += new System.EventHandler
    (this.ComputeCost_CheckedChanged);

// radInterm
this.radInterm.Checked = true;
this.radInterm.Location = new
    System.Drawing.Point(16, 56);
this.radInterm.Name = "radInterm";
this.radInterm.Size = new
    System.Drawing.Size(136, 24);
this.radInterm.TabIndex = 1;
this.radInterm.TabStop = true;
this.radInterm.Text = "Intermediate";
this.radInterm.Click += new System.EventHandler
    (this.ComputeCost_CheckedChanged);
```
```