# Dog Sales in the Western Region

![](bbox=[0.151, 0.131, 0.74, 0.431])

Dog Sales in the Eastern Region

Dog Sales in the Northern Region

![](bbox=[0.151, 0.475, 0.74, 0.546])

**FIGURE 16-9:** Chart embedded with binary stream rendering

The binary stream rendering is another simple solution to embed chart images into a legacy website. You do not have to touch the .aspx page. You create the referencing page with an HTML `<img>` tag. Listing 16-10 shows an example.

+   **LISTING 16-10:** BinaryStreamRendering.htm

```
```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>Chart in a legacy web site with binary streaming/</title>
</head>
<body>
  <h2>Dog Sales in the Southern Region</h2>
  <img src="DogSalesChart.aspx?region=South" height="500px" width="800px" alt="Southern Region" />
</body>
</html>
```
```

Code file |BinaryStreamRendering.htm| available for download at Wrox.com