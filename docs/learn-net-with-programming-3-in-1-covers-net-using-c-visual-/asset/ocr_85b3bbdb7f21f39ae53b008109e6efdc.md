```
Xmlelement name = xmldoc.createelement("Name");

Name.innertext = textbox1.Text;

Xmlelement Emp_id = xmldoc.createelement("Emp_id");

Emp_id.innertext = textbox2.Text;

Xmlelement Qualification = xmldoc.createelement("Qualification");

Qualification.innertext = dropdownlist1.selecteditem.Text;

Parentelement.appendchild(name);

Parentelement.appendchild(Emp_id);

Parentelement.appendchild(Qualification);

Xmldoc.documentelement.appendchild(parentelement);

Xmldoc.Save(Server.mappath("Employee.xml"));

Binddatalist();
}
```

# Step 7: Run your application by pressing F5. The output is:

Save.jpg