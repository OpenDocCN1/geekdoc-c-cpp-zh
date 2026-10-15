# SITE COLLECTIONS, SITES, AND WEBS

In regard to scope, you should be aware of a naming inconsistency. This issue will also be apparent when you begin to write code against the SharePoint object models. What we call site collections and sites today were formerly called sites and webs, respectively. These legacy terms remain in the XML schemas and developer object models we use today. Therefore, when you want to activate a Feature at the site level, you set the scope to Web. When you want to activate it at the site collection level, you set the scope to Site. This will be somewhat confusing when you first start developing on the SharePoint platform but it will become second nature in no time.

Also contained in the feature manifest are references to the associated element manifests which describe the contents of the Feature. For our sample Feature there will only be one element manifest but it will define three elements. The first (a ListInstance) will create the list of contacts and populate it with some data. The second (a Module) will add the page you will create shortly to the target site, and the third (a CustomAction) will add a link to the page in the Site Actions menu.

# Creating the Element Manifest

To create the element manifest, create a new file named `elements.xml`, save it to the SimpleFeature folder, and add the following code:

```
```xml
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

  <!-- Create the contacts list -->
  <ListInstance
    FeatureId="00BFEA71-7E6D-4186-9BA8-C047AC750105"
    TemplateType="105"
    Title="Contacts"
    Url="Contacts"
    QuickLaunchUrl="Contacts/Forms/AllItems.aspx">
    <Data>
      <Rows>
        <Row>
          <Field Name="ID">1</Field>
          <Field Name="Last Name">Anders</Field>
          <Field Name="First Name">Maria</Field>
          <Field Name="Company">Alfreds Futterkiste</Field>
          <Field Name="Business Phone">030-0074321</Field>
        </Row>
        <Row>
          <Field Name="ID">2</Field>
          <Field Name="Last Name">Hardy</Field>
          <Field Name="First Name">Thomas</Field>
          <Field Name="Company">Around the Horn</Field>
          <Field Name="Business Phone">(171) 555-7788</Field>
        </Row>
        <Row>
          <Field Name="ID">3</Field>
          <Field Name="Last Name">Lebihan</Field>
          <Field Name="First Name">Laurence</Field>
          <Field Name="Company">Bon app'</Field>
          <Field Name="Business Phone">91.24.45.40</Field>
        </Row>
        <Row>
          <Field Name="ID">4</Field>
          <Field Name="Last Name">Ashworth</Field>
          <Field Name="First Name">Victoria</Field>
          <Field Name="Company">B's Beverages</Field>
          <Field Name="Business Phone">(171) 555-1212</Field>
        </Row>
```
```