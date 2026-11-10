
- 2. Select the DATA TYPE radio button, provide a name for your data element in the field to the right of the button, and click the CREATE button. Because the data elements are repository objects, they should exist in a customer namespace (i.e., the data element name should start with Z or Y; see Figure 4.8).

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_130_0.png)

**Figure 4.8** ABAP Data Dictionary: Initial Screen

- 3. The system presents a dialog box (see Figure 4.9) asking you to select the data type you want to create. DATA ELEMENT represents the user-defined elementary data type, so select the DATA ELEMENT radio button and click CONTINUE (green checkmark). (We’ll have an opportunity to explore structures and table types in later chapters.)

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_130_1.png)

**Figure 4.9** Create Type

- 4. On the next screen (see Figure 4.10), provide a short description for your data type to help others understand its purpose. This short text is also displayed as a title in the `F1` help for all screen fields referring to this data element.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_132_0.png)

**Figure 4.11** Data Type Value List

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_132_1.png)

**Figure 4.12** Activating a Data Element

- 8. If the data type supports decimals, you can also maintain the number of decimal places in the DECIMAL PLACES field.

The data type we just created has global visibility and can be used to define data objects or user-defined data types in any program, as shown:

```abap
DATA name TYPE ZCB_PERSON.
TYPES user TYPE ZCB_PERSON.
```

If you change the definition of the data element, the changes will be automatically reflected for all the objects referring to that data element. This allows you to centrally maintain the definitions of all related objects. Because data elements are global objects, it’s recommended not to change them without analyzing the impact first.

There are many things that can be maintained at the data element level, like search helps, field labels, and help documentation. The program fields can derive these properties automatically. We’ll explore these concepts in greater detail in Chapter 10.

## 4.4.3 Domains

*A domain* describes the technical attributes of a field. The primary function of a domain is to define a value range that describes the valid data values for the fields that refer to this domain.

However, if you plan to create multiple data elements that are technically the same, you can attach a domain to derive the technical attributes of a data element. This allows you to manage the technical attributes of multiple data elements centrally, meaning that you can change the technical attributes once for the domain, and the change will be reflected automatically for all the data elements that use the domain. This is an alternative to changing each individual data element to maintain technical attributes when a predefined elementary data type is selected.

A field can't be referred to a domain directly; it picks up the domain reference through a data element if the domain is attached to the data element. In other words, you always attach a domain to a data element. Figure 4.13 depicts this relationship.

In Figure 4.13, Field 1 refers to Data Element 1, whereas Field 2 and Field 3 refer to Data Element 2. Both Data Element 1 and Data Element 2 are using the same domain to derive technical attributes. This implies that Field 2 and Field 3 are both semantically and technically the same, whereas Field 1 is *semantically* different from Field 2 and Field 3 but is *technically* the same as these two fields.

For example, a sales document number and a billing document number can both be technically the same, such as both being ten-digit character fields. However, the sales document and billing document are semantically different (i.e., their purposes are different). For such a case, you can use the same domain for both the sales document number and billing document number but a separate data element for each.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_134_0.png)

**Figure 4.13** Fields, Data Elements, and Domain Relationships

You can also maintain a *conversion routine* at the domain level for automatic conversion to internal and external data formats for fields referring to a domain. We’ll discuss this topic more in Chapter 10.

You can take a *top-down* approach or a *bottom-up* approach to create a domain; that is, you either can create the domain separately first and attach it to a data element or can create the domain while creating the data element. Let’s take a bottom-up approach to create a domain and attach it to the previously created data element `ZCB_PERSON`.

Because domains and data elements have their own namespaces, you can use the same name for both of them. In the following example, you’ll create a domain using the same name as the data element created previously in Section 4.4.2; you can use a different name if it becomes too confusing.

The following steps will walk you through the procedure to create a domain in ABAP Data Dictionary:

- 1. On the initial ABAP Data Dictionary screen (Figure 4.14), select the DOMAIN radio button, input the name of the domain, and click the CREATE button. Domains are also repository objects, so they should exist in a customer namespace.
- 2. Enter a SHORT DESCRIPTION for the domain. This short description is never seen by end users. It’s displayed when searching for domains using `F4` help and it helps other developers understand your domain’s purpose.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_135_0.png)

**Figure 4.14** ABAP Dictionary: Initial Screen

- 3. Use the `F4` help for the DATA TYPE field to select the data type and enter a value for the No. Characters field. This value defines the field length (Figure 4.15). Optionally, you can enter the number of Decimal Places for numeric types.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_135_1.png)

**Figure 4.15** Change Domain Screen

- 4. You can also enter Output Characteristics like output length, conversion routine, or disabling automatic uppercase conversion for screen fields referring to this domain. We'll explore these options further in Chapter 10.
- 5. Activate the domain. To attach this domain to a data element, open the data element and select the DOMAIN radio button under the ELEMENTARY TYPE radio button, as shown in Figure 4.16. Type the name of the domain and press `Enter`.
- 6. Notice that the DATA TYPE and LENGTH are chosen by the system automatically. If the system does not set the DATA TYPE and LENGTH after pressing the `Enter` key, it means the domain does not exist, and an informative message, NO ACTIVE DOMAIN [DOMAIN_NAME] AVAILABLE, is displayed.

  At this point, you can simply double-click the domain name to create it using the top-down approach.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_136_0.png)

**Figure 4.16** Attaching Domain to Data Element

## 4.4.4 Data Objects

Data objects derive their technical attributes from data types and occupy memory space to store the work data of a program. ABAP statements access this content by addressing the name of the data object. Data objects exist as an instance of data types. Each ABAP data object has a set of technical attributes, such as data type, field length, and number of decimal places.

Data objects are the physical memory units with which your ABAP statements can work. ABAP statements can address and interpret the contents of data objects. All data objects are declared in the ABAP program and are local to the program, which means they exist in the program memory and can be accessed only from within the same program. There is no concept of defining data objects centrally in the system.

Data objects are not persistent; they exist only while the program is being executed. The life of the data object lasts only as long as the program execution lasts. They are created when the program execution starts and destroyed when the program execution ends.

Before you can process persistent data (such as data from a database or a sequential file), you must read the data into data objects first, which can then be accessed by ABAP statements. Similarly, if you want to retain the contents of a data object beyond the end of the program, you must save it in a persistent form. Technically, anything that can store work data in a program can be called a data object.

Let’s explore different kinds of data objects that can be defined in your ABAP programs. In the following subsections, we will look at the different classifications of data objects.

### Literals

*Literals* are not created using any declarative statements, nor do they have names. They exist in the program source code and are called *unnamed data objects*. Like all data objects, they have fixed technical attributes.

You cannot access the memory of a literal to read its content, because it’s an unnamed data object. This means that literals are not reusable data objects and their contents can’t be changed. Unlike literals, all other data objects are named data objects, which are explicitly declared in the program.

For example, in the following snippet, `Hello World` and `1234` are literals:

```
WRITE 'Hello World'.
WRITE 1234.
```
