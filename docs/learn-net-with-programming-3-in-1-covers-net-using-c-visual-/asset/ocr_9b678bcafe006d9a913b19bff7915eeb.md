```
1. 19.
    Response.Cookies["computer"]["dell"] = "dell";
19. If (lenevo.Checked)
20. Response.Cookies["computer"]["lenevo"]     =
    "lenevo";
21. If (acer.Checked)
22. Response.Cookies["computer"]["acer"] = "acer";
23. If (sony.Checked)
24. Response.Cookies["computer"]["sony"] = "sony";
25. If (wipro.Checked)
26. Response.Cookies["computer"]["wipro"]     =
    "wipro";
27. // ------------ Fetching Cookies -------------------
    //
28. If  (Request.Cookies["computer"].Values.tostring()
    != null)
29. {
30. If (Request.Cookies["computer"]["apple"] != null)
31. Label2.Text                         +=
    Request.Cookies["computer"]["apple"] + " ";
32. If (Request.Cookies["computer"]["dell"] != null)
33. Label2.Text                         +=
    Request.Cookies["computer"]["dell"] + " ";
34. If (Request.Cookies["computer"]["lenevo"] != null)
35. Label2.Text                         +=
    Request.Cookies["computer"]["lenevo"] + " ";
36. If (Request.Cookies["computer"]["acer"] != null)
37. Label2.Text                         +=
    Request.Cookies["computer"]["acer"] + " ";
38. If (Request.Cookies["computer"]["sony"] != null)
```