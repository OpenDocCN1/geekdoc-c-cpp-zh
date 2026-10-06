# Implementing Custom Models

Qt's predefined models offer a convenient means of handling and viewing data. However, some data sources cannot be used efficiently with the predefined models, and for these situations it is necessary to create custom models optimized for the underlying data source.

Before we embark on creating custom models, let's first review the key concepts in Qt's model/view architecture. Every data element in the model has a model index and a set of attributes, called roles, that can take arbitrary values. We saw earlier in the chapter that the most commonly used roles are `Qt::DisplayRole` and `Qt::ToolTip`, `Qt::StatusTipRole`, and `Qt::WhatsThisRole`, and yet others for supplementary data (e.g., controlling basic display attributes as `Qt::FontRole`, `Qt::TextAlignmentRole`, `Qt::ColorRole`, and `Qt::BackgroundColor`). For a list model, the only relevant index component is the row number, and for a table model, the relevant index components are the row and column numbers, accessible from `QModelIndex::row()` and `QModelIndex::column()`

For both list and table models, every item's parent is the root, which is represented by an invalid QModelIndex. The first two examples in this section show how to implement custom table models.

A tree model is similar to a table model, with the following differences: Like a table model, the parent of top-level items is the root (an invalid QModelIndex), but every item's parent is some other item in the hierarchy. Parents are accessible from `QModelIndex::parent()`. Every item has its role data, and zero or more children, each item in its own right. Since items have other items as children, it is possible to represent recursive (tree-like) data structures, as the final example in this section will show. Figure 10.9 shows a schematic of the different models.

# Figure 10.9. Schematic view of Qt's models

![](bbox=[0.023, 0.725, 0.976, 0.925])

The first example in this section is a read-only table model that shows currency values in relation to each other. The application is shown in Figure 10.10.