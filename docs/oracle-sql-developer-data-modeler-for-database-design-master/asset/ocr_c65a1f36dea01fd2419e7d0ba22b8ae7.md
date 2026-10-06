# 78 Oracle SQL Developer Data Modeler for Database Design Mastery

![](bbox=[0.135, 0.115, 0.836, 0.506])

FIGURE 4-14. Selecting entities and relationships for the unique key

+   - An SSN can be changed. When you move to another country, you are given a temporary SSN. When you get citizenship, you get a permanent one. There are plenty of cases when an SSN has changed.

+   - An SSN is not something you can define yourself; it comes from another system and is controlled by other organizations and their rules. What if they change the rules? Do not use primary keys from another system's data (history data, and so on).

+   - An SSN is defined many times as sensitive data, redaction, or masking in several tables (of foreign keys), which is not very efficient.

When selecting the primary key, you have two choices: natural key or surrogate key. Which one is better? The only correct answer to any question about modeling issues is: it depends. But deciding on the primary key is one of the most important