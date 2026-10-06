# Chapter 2: Getting Started with Oracle SQL Developer Data Modeler 27

# Creating or Editing a Glossary

You can create and edit a glossary in the Glossary Editor (choose Tools | Glossary Editor), as shown in Figure 2-12. The default directory for saving glossaries is set in the Default Import Directory preference.

If you want to edit an existing glossary, open the Glossary Editor, select the glossary file, make your changes, and click Save. This file can be a .csv or .txt file made with ERwin.

If you want to create a new glossary, start the Glossary Editor and define a filename that does not exist. Data Modeler will automatically create that file as a new glossary. Every glossary should have a name and a description. By selecting Incomplete Modifiers, you will allow modifiers and qualifiers to be named outside the glossary definitions, so those names do not need to be in the glossary. If you select Case Sensitive, all the validation is based on the fact that the name under validation must be written the same way as the word in the glossary. By selecting Unique Abbreviations, you will have control over the whole glossary in that all the abbreviations in the glossary will be unique. The same abbreviation cannot be used in several words, and there cannot be a word without an abbreviation. The name validation process will report these cases. With Separator and Sep. Char., you

![](bbox=[0.136, 0.501, 0.833, 0.856])

FIGURE 2-12. Glossary Editor