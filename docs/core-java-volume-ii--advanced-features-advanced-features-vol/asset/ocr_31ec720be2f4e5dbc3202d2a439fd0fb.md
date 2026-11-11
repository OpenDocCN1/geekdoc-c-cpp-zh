```
```java
return Printable.PAGE_EXISTS;
}
}, flavor, null);
DocPrintJob job = service.createPrintJob();
var attributes = new HashPrintRequestAttributeSet();
job.print(doc, attributes);
} else {
System.out.println("No factories for " + mimeType);
}
}
}
}
```
```

# ### 11.5.5 Printing Attributes

The print service API contains a complex set of interfaces and classes to specify various kinds of attributes. There are four important groups of attributes. The first two specify requests to the printer.

+   - Print request attributes request particular features for all doc objects in a print job, such as two-sided printing or the paper size.
+   - Doc attributes are request attributes that apply only to a single doc object.

The other two attributes contain information about the printer and job status.

+   - Print service attributes give information about the print service, such as the printer make and model or whether the printer is currently accepting jobs.
+   - Print job attributes give information about the status of a particular print job, such as whether the job is already completed.

To describe the various attributes, there is an interface Attribute with subinterfaces:

```
```
PrintRequestAttribute
DocAttribute
PrintServiceAttribute
PrintJobAttribute
SupportedValuesAttribute
```
```

Individual attribute classes implement one or more of these interfaces. For example, objects of the Copies class describe the number of copies of a printout. That class implements both the PrintRequestAttribute and the PrintJobAttribute interfaces. Clearly, a print request can contain a request for multiple copies. Conversely, an attribute of the print job might be how many of these copies were actually printed. That number might be lower, perhaps because of printer limitations or because the printer ran out of paper.