# 35

# Creating Documents with WPF

# What’s In This Chapter?

+   - Using text elements
+   - Creating flow documents
+   - Creating fixed documents
+   - Creating XPS documents
+   - Printing documents

# Wrox.com Code Downloads For This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

+   - Show Fonts
+   - Text Effects
+   - Table
+   - Flow Documents
+   - Create XPS
+   - Printing

# Introduction

Creating documents is a large part of WPF. The namespace System.Windows.Documents supports creating both flow documents and fixed documents. This namespace contains elements with which you can have a rich Word-like experience with flow documents, and create WYSIWYG fixed documents.

*Flow documents* are geared toward screen reading; the content of the document is arranged based on the size of the window, and the flow of the document changes if the window is resized. *Fixed documents* are mainly used for printing and page-oriented content and the content is always arranged in the same way.

This chapter teaches you how to create and print flow documents and fixed documents, and covers the namespaces System.Windows.Documents, System.Windows.Xps, and System.IO.Packaging.

# Text Elements