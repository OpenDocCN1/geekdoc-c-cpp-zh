# Example E.18.

```
DialogResult result = MessageBox.Show("Place message here",
    "Place caption here", MessageBoxButtons.OK);

if (result == DialogResult.OK) {
    PlaySound(@"C:\SourceCode\Fire.wav", 0, 0);
}
```

# Example E.19.

```
DialogResult result = MessageBox.Show("Place message here",
    "Place caption here", MessageBoxButtons.OKCancel);

if (result == DialogResult.Cancel) {
    PlaySound(@"C:\SourceCode\Fire.wav", 0, 0);
}
```

# Example E.20.

```
DialogResult result = MessageBox.Show("Place message here",
    "Place caption here", MessageBoxButtons.YesNo);

if (result == DialogResult.Yes) {
    PlaySound(@"C:\SourceCode\Fire.wav", 0, 0);
}
```

# Example E.21.

```
DialogResult result = MessageBox.Show("Place message Here",
    "Place caption here", MessageBoxButtons.YesNo);

if (result == DialogResult.No) {
    PlaySound(@"C:\SourceCode\Fire.wav", 0, 0);
}
```

# Example E.22.

```
DialogResult result = MessageBox.Show("Place message here",
    "Place caption here", MessageBoxButtons.YesNoCancel);

if (result == DialogResult.Cancel) {
    PlaySound(@"C:\SourceCode\Fire.wav", 0, 0);
}
```