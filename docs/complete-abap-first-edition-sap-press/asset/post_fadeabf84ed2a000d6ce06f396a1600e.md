
| ITEM_ID | LANGUAGE | DESCRIPTION | QUANTITY | UOM |
|---|---|---|---|---|
| 1 | English | Pen | 10 | PC |
| 1 | German | Stift | 10 | PC |
| 2 | English | Pencil | 20 | Box |
| 2 | German | Bleistift | 20 | Box |
| 3 | English | Paper | 10 | KG |
| 3 | German | Papier | 10 | KG |

**Table 2.3** TB_ITEM Expanded to Accommodate Language Key

In Table 2.3, the ITEM_ID field is no longer unique. The primary key of the table should always be unique, so the key of this table should be expanded to include the LANGUAGE field as well. Therefore, the key of Table 2.3 is a combination of the ITEM_ID and LANGUAGE fields. Individually, the data in ITEM_ID field can repeat n number of times and the data in LANGUAGE field can repeat n number of times, but the combination should always be unique.

As you may have noticed, in Table 2.3 we're repeating the same data multiple times to accommodate various languages. When more languages are added to the mix, you end up with redundant data. What if we could separate the descriptions and maintain them in a separate table that can be linked to this table with foreign keys?

Table 2.4 stores the item details, and Table 2.5 stores the descriptions in multiple languages. This arrangement of tables avoids data redundancy, and because the tables are now linked through a foreign key, we can query Table 2.5 for the description in the preferred language using the ITEM_ID field of Table 2.4.

| ITEM_ID | QUANTITY | UOM |
|---|---|---|
| 1 | 10 | PC |
| 2 | 20 | Box |
| 3 | 10 | KG |

**Table 2.4** TB_ITEM without Description

| ITEM_ID | LANGUAGE | DESCRIPTION |
|---|---|---|
| 1 | English | Pen |
| 1 | German | Stift |
| 2 | English | Pencil |
| 2 | German | Bleistift |
| 3 | English | Paper |
| 3 | German | Papier |

**Table 2.5** New Storing Item Descriptions

This is how you model data in an SAP system. For example, the material master data is stored in table `MARA`, the material description in multiple languages is stored in table `MAKT`, and the plant data for material is stored in table `MARC`. With this arrangement, you can query different tables to get different information about the material using the foreign key concept.

In this section, we discussed the different layers of SAP's three-tier architecture in detail. [Figure 2.7](#figure-2-7) summarizes the three layers of the SAP system.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_62_0.png)

**Figure 2.7** Overview of Three Layers

As shown in [Figure 2.7](#figure-2-7), the application server includes a special area called the *buffer*. A buffer acts like a cache in which data that is frequently accessed but seldom changed can be stored. This allows you to improve the performance of the applications, because the data can be accessed from the local buffer. A buffer also helps to reduce the database and network load, as the application server need not access the database repeatedly for the same information.

Buffering data is recommended when data in the tables does not change frequently and having access to up-to-date data is not critical for the application. If any data changes in the database table, a background process will update the buffer at a fixed interval. This means that buffering a frequently changing table is counterproductive.

In the next section, we’ll look at data structures and clients.

## 2.3 Data Structures

The SAP system typically contains various data, such as master data, user data, and transaction data. Each SAP system further consists of multiple *clients*. *A client* represents an organizational unit in an SAP system.

In SAP systems, the following terms must be differentiated with regard to the data structure:

- **Client-specific data**: Data that exists within a specific client of the system
- **Cross-client (client-independent) data**: Data that exists across all the clients of the system.

In other words, when we store any data in an SAP system, the data can be specific to a client or it can be accessed centrally from any client.

In this section, we will discuss the concept of a client, the significance of using different clients, and how our decisions about clients influence the data stored in an SAP system.

### 2.3.1 Client Overview

Each SAP system can be divided into multiple clients, and each client is identified by a three-digit numeric value. Each client has its own master data, user data, and transactional data. The data in a client is known as *client-specific data*.

Each SAP system logon must include a client ID (see Figure 2.8), which indicates a logon to a specific client.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_64_0.png)

**Figure 2.8** Client ID on Logon Screen

### 2.3.2 Client-Specific and Cross-Client Data

As mentioned previously, data in an SAP system is either client-specific or cross-client. Client-specific data is visible only in the client in which the data was created, whereas cross-client data is accessible from any client in the system.

Because the data in an SAP system is always stored in a database table, the data is restricted to a client by maintaining a client column (field) in the application table. These tables are called client-specific tables and the client columns (see Figure 2.9) are called MANDT.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_64_1.png)

**Figure 2.9** Client Field in Table

The MANDT field stores the current client number in which the data is generated. While accessing the data from the client-specific tables, the system automatically matches the user's current client with the MANDT field of the table, restricting the data to the current client.

For example, say a purchase order is created while logged on to client 100. The relevant purchase order application-related database tables update with the new purchase order data, and the MANDT fields of those tables will be updated with the client number (100 in this case) automatically. If you try to open the purchase order in another client—say, client 200—the system won't show the purchase orders created in client 100, because it will try to match the MANDT field with 200.

For cross-client tables, the MANDT field isn't part of the table key, so the data isn't restricted to the client. The data can be accessed from any client of the system. To find out if the data in a table is client-dependent or cross-client, check if the table has MANDT as the first field and as part of the key, as shown in Figure 2.9.

For example, say that the material master table MARA has MANDT as the first field and part of the table key. This makes table MARA client-specific. If you create a new material in client 100, then the material data is visible only in client 100. You can't access this data from other clients of the system. Similarly, if the material data is changed in a particular client, then the change won't affect the data in other clients of the system. Application data is generally client-specific, and customizing data is generally cross-client.

The client concept entails splitting your SAP system into multiple clients and separating the data by either restricting it to a particular client or keeping it cross-client.

When you log on to an SAP system, you're logging onto a particular client. Any activities carried out in the system are always carried out in one specific client. When planning the SAP system landscape, you can create various clients for various activities. For example, you can have one client for development, one client for testing (QA), and one client for production.

Some of the most important client roles are as follows:

- **Customizing and development client (CUST)**: The SAP system software is standard business software and is adapted to company-specific business requirements when implemented. To customize the SAP software and carry out various development activities, each SAP system has a CUST client.
- **Quality assurance client (QTST)**: Once the developments are completed in CUST, they need to be tested thoroughly before the application can be used in production. The client in which these tests are carried out is called QTST. The QTST client is generally refreshed with production data at regular intervals so that applications can be tested with more realistic production data.
- **Production client (PROD)**: The production environment uses a different client, PROD. PROD is where actual business activities take place. There are no development or testing activities in this client in order to ensure smooth business operations.

These three clients (CUST, QTST, and PROD) are central clients that exist in every system landscape. In general, these three clients are maintained in separate systems and SAP instances, with some transportation mechanism in place to move objects between clients.

Each system will have precisely one client for each of these client roles. The development system will have a CUST client, the quality system will have a QTST client, and the production system will have a PROD client.

For example, ABAP programs are cross-client. When you create a program in one client, it is made automatically available in all the clients of that system. If you change the program in a CUST client, the changes automatically will be reflected in the QTST and PROD clients (if all the clients are set up in the same SAP instance). If all clients are set up in the same instance, you won't have the opportunity to test your program changes. By keeping the clients in separate systems, you can make your changes in the development system, transport them to the quality system for testing, and once you're satisfied, import them to the production system.

In order to maintain consistency across clients, we recommend that all the Customizing settings be carried out in a single Customizing client and transported (with the Change and Transport System [CTS]) to other clients. This helps prevent situations in which applications behave differently in different clients due to different customization settings.
