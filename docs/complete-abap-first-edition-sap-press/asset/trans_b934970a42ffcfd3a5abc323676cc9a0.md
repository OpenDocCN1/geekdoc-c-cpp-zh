
```abap
REPORT ZCB_EXAMPLE.
*Global declarations of the program.
DATA: f1 TYPE c VALUE 'A',
      f2 TYPE c VALUE 'B'.
*&--------------------------------------------------------------*
*&     Form OUTPUT
*&--------------------------------------------------------------*
FORM output.
*Local declaration that can be accessed (visible) within
*this subroutine
  DATA f3 TYPE c VALUE 'C'.
  WRITE f1.
  WRITE f2.
  WRITE f3.
ENDFORM.
END-OF-SELECTION.
  PERFORM output. "Calling a subroutine
```

**清单 7.2** 更改处理块的顺序

执行完处理块中的代码后，控制权将返回给它的调用者。

## 结束处理块

处理块的执行在最后一条语句执行完毕后结束。但是，也可以通过使用某些语句（如 `CHECK`、`EXIT` 或 `RETURN`）以编程方式结束它。例如，在检查某个条件后，如果条件不满足时你不想执行处理块中的剩余代码，那么可以使用 `CHECK`、`EXIT` 或 `RETURN` 语句结束处理块，而不执行该处理块中的剩余代码。

如果在循环语句（`DO` 循环、`WHILE` 循环、`LOOP AT` 等）内部使用 `CHECK` 和 `EXIT` 语句，它们的行为会有所不同。当这些语句在循环内使用时，它们不会结束处理块；它们只影响循环处理。例如，`CHECK` 语句在循环中使用时，会退出当前循环并处理下一次迭代。

然而，`EXIT` 语句会完全退出循环处理。`EXIT` 和 `CHECK` 语句在循环处理之后都会继续执行处理块中的剩余代码。`RETURN` 语句无论在循环内还是循环外使用，都总是退出处理块。

无论处理块如何结束，每次终止时控制权都会返回给处理块的调用者。

清单 7.3 展示了 `EXIT` 语句的用法。在清单 7.3 中，我们在子例程 `OUTPUT` 内使用 `EXIT` 语句。位于 `EXIT` 语句之后的 `WRITE f3` 语句将不会执行，因为程序到达 `EXIT` 语句时会退出处理块。

```abap
REPORT ZCB_EXAMPLE.
DATA : f1 TYPE c VALUE 'A',
       f2 TYPE c VALUE 'B'.
END-OF-SELECTION.
  PERFORM output. "Calling a subroutine
*&---------------------------------------------------------------------*
*&      Form  OUTPUT
*&---------------------------------------------------------------------*
  FORM output.
  DATA f3 TYPE c VALUE 'C'.
    WRITE f1.
    WRITE f2.
  EXIT.
    WRITE f3.
  ENDFORM.
```

**清单 7.3** 在处理块内使用 EXIT 语句

清单 7.4 展示了一个在循环内使用 `EXIT` 语句的示例。在此示例中，我们在 `DO` 循环内使用 `EXIT` 语句。在第一轮循环之后，系统在遇到 `EXIT` 语句时会退出循环，但会继续执行子例程中的剩余代码。

因此，在这种情况下，语句 `WRITE f3` 将被执行。

```abap
REPORT ZCB_EXAMPLE.
DATA : f1 TYPE c VALUE 'A',
       f2 TYPE c VALUE 'B'.
END-OF-SELECTION.
  PERFORM output. "Calling a subroutine
*&---------------------------------------------------------------------*
*&      Form  OUTPUT
*&---------------------------------------------------------------------*
  FORM output.
  DATA f3 TYPE c VALUE 'C'.
  DO 3 TIMES.
    WRITE f1.
    WRITE f2.
  EXIT.
ENDDO.
  WRITE f3.
ENDFORM.
```

**清单 7.4** 循环内的 EXIT 语句

**清单 7.5** 展示了使用 `CHECK` 语句退出处理块的示例。在此示例中，我们使用 `CHECK` 语句检查数据对象 f2 和 f3 的内容是否不匹配。

如果条件满足，将执行处理块的剩余代码；否则系统将退出处理块，不再执行处理块中的后续代码。在我们的示例中，语句 `WRITE f3` 不会执行，因为 f2 和 f3 的值相同。

```abap
REPORT ZCB_EXAMPLE.
DATA : f1 TYPE c VALUE 'A',
       f2 TYPE c VALUE 'B'.
END-OF-SELECTION.
  PERFORM output. "Calling a subroutine
*&---------------------------------------------------------------------*
*&      Form  OUTPUT
*&---------------------------------------------------------------------*
FORM output.
  DATA f3 TYPE c VALUE 'B'.
  WRITE f1.
  WRITE f2.
  CHECK f2 <> f3.
  WRITE f3.
ENDFORM.
```

**清单 7.5** 在处理块中使用 CHECK 语句

**清单 7.6** 展示了一个在循环内使用 `CHECK` 语句的示例。在该示例中，我们在 `DO` 循环内使用 `CHECK` 语句检查数据对象 f1 和 f2 的内容是否相同。

当系统遇到 `CHECK` 语句时，只有在 `CHECK` 条件满足时才会执行 `CHECK` 语句之后的语句。如果条件不满足，系统将跳到下一次循环遍历，而不执行当前循环遍历中的后续代码。

循环处理完成后，系统将继续执行处理块中的剩余代码。因此，在此示例中，`WRITE f1` 语句执行三次，`WRITE f2` 语句从不执行，`WRITE f3` 语句执行一次。

```abap
REPORT ZCB_EXAMPLE.
DATA : f1 TYPE c VALUE 'A',
       f2 TYPE c VALUE 'B'.
END-OF-SELECTION.
  PERFORM output. "Calling a subroutine
*&---------------------------------------------------------------------*
*&      Form  OUTPUT
*&---------------------------------------------------------------------*
FORM output.
  DATA f3 TYPE c VALUE 'B'.
  DO 3 TIMES.
    WRITE f1.
    CHECK f1 = f2.
    WRITE f2.
  ENDDO.
  WRITE f3.
ENDFORM.
```

**清单 7.6** 循环内的 CHECK 语句

**清单 7.7** 展示了一个使用 `RETURN` 语句的示例。在此示例中，我们在 `DO` 循环内使用 `RETURN` 语句。因为 `RETURN` 语句无论在循环内还是循环外使用，都总是退出处理块，所以 `WRITE f1` 语句执行一次，而 `WRITE f2` 和 `WRITE f3` 语句从不执行。

```abap
REPORT ZCB_EXAMPLE.
DATA : f1 TYPE c VALUE 'A',
       f2 TYPE c VALUE 'B'.
END-OF-SELECTION.
  PERFORM output. "Calling a subroutine
*&---------------------------------------------------------------------*
*&      Form  OUTPUT
*&---------------------------------------------------------------------*
FORM output.
  DATA f3 TYPE c VALUE 'B'.
  DO 3 TIMES.
    WRITE f1.
    RETURN.
    WRITE f2.
  ENDDO.
  WRITE f3.
ENDFORM.
```

**清单 7.7** RETURN 语句

## 语句

除全局数据声明（也称为 *虚拟处理块*）外，所有 ABAP 程序语句都属于某个处理块。如果你在全局声明区域和处理块之间编写任何语句（该语句没有显式分配给某个处理块，并且不是声明性语句），它们会自动分配给 `START-OF-SELECTION` 处理块的开头。`START-OF-SELECTION` 处理块在可执行程序中扮演默认处理块的角色。

`Listing 7.8` 包含使用各种处理块的示例代码。这里，我们显示给定开票凭证编号的行项目数据。

```abap
TYPES: BEGIN OF ty_vbrp,
       vbeln TYPE vbeln_vf,  "Document Number
       posnr TYPE posnr,     "Item Number
       fkimg TYPE fkimg,     "Quantity
       vrkme TYPE vrkme,     "UoM
       netwr TYPE netwr,     "Net Value
       matnr TYPE matnr,     "Material Number
       arktx TYPE arktx,     "Description
       mwsbp TYPE mwsbp,     "Tax Amount
     END OF ty_vbrp.

DATA : it_vbrp TYPE STANDARD TABLE OF ty_vbrp,
       wa_vbrp LIKE LINE OF it_vbrp,
       v_vbeln TYPE vbeln_vf.

PARAMETERS p_vbeln TYPE vbeln_vf.

INITIALIZATION. "Event Block
AUTHORITY-CHECK OBJECT 'V_VBRK_FKA'
          ID 'FKART' FIELD 'F2'
          ID 'ACTVT' FIELD '03'.
IF sy-subrc <> 0.
* Implement a suitable exception handling here
  MESSAGE 'Authorization check failed' TYPE 'E'.
ENDIF.

AT SELECTION-SCREEN. "Event Block
  SELECT SINGLE vbeln FROM vbrk
                   INTO v_vbeln
                   WHERE vbeln EQ p_vbeln.
IF sy-subrc IS NOT INITIAL.
  MESSAGE 'Invalid Document Number' TYPE 'E'.
ENDIF.

START-OF-SELECTION. "Event Block
```
