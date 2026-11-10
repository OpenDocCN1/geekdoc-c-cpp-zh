In this chapter, we'll explain how to create forms using the three primary SAP form technologies. We'll describe the process and provide step-by-step examples.

# 18 Forms

Forms print application data. Reports are typically used to process data in a user-driven fashion and display the result on the screen. With forms, we process the data from the database and print the output. Because reports also provide the ability to print the output, you may ask, “Why exactly do we need forms?” With reports, you're limited to displaying the data in a tabular or hierarchical format, but forms provide more control over how you print the output.

If you've ever seen an invoice, you may have noticed that the data on the invoice isn’t exactly in a tabular format. An invoice typically has many sections (or windows) in which different information is printed. For example, one window on the top right might show invoice details such as the invoice number, payment due date, and so on. Another window on the top left might show customer details and shipping information. The main section in the center of the page might show item details and the like.

Figure 18.1 shows a typical invoice: you can see the invoice data printed across various sections of the page.

Forms generally are used to print document data such as sales orders, invoices, delivery documents, and so on. Sometimes, there is a legal requirement to print these documents in a specific format. With form development, we use a layout designer that helps format the page for printing.

There are three different technologies available to develop forms: SAPscripts, smart forms, and SAP Interactive Forms by Adobe. Each new technology has attempted to make developing and maintaining forms easy. The oldest among them is SAPscripts, which always was and still is a pain to develop and has a lot of limitations. We'll discuss SAPscripts in Section 18.1.