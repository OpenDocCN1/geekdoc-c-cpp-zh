

## 6.9.2 多项式加法

设两个多项式 A 和 B 为

```
A = 4x^0 + 3x^6 + 5x^2 + 1
B = 3x^6 + x^2 - 2x
```

多项式 A 和 B 相加得到多项式 C。这里假设两个多项式存储在按指数降序排列的链表中。

两个多项式 A 和 B 存储在两个链表中，指针 ptr1 和 ptr2 分别指向各多项式的第一个节点。要相加这两个多项式，让我们使用笔算法。让我们使用这两个指针 ptr1 和 ptr2 沿着 A 和 B 的各项移动。

### 笔算法

如果两项的指数相等，则将它们的系数相加，并为结果多项式 C 创建一个新项。如果 A 中当前项的指数小于 B 中当前项的指数，则复制 B 中的项并将其附加到 C。指针 ptr2 移动到下一项。如果 A 中当前项的指数大于 B 中当前项的指数，则对 A 采取类似操作。

每次生成新节点时，其指数和系数字段会相应设置，并将结果项附加到结果多项式 C 的末尾。对于多项式 C，我们有 ptr3 沿着结果多项式 C 移动。它始终指向新追加的项，即指向 C 的最后一项。这样可以避免每次附加节点时遍历列表 C。将节点附加到多项式与在列表末尾插入节点相同。只有在添加第一个节点时，才会执行适当的步骤来初始化 ptr3。

将项 NewTerm 附加到多项式（例如 C）的算法如下，使用指针 ptr3：

- 1. if(c_ptr = NULL)
   则 c_ptr = NewTerm;
   否则
   c_ptr->link = NewTerm;
   c_ptr = NewTerm;
- 2. 停止

### 多项式加法算法

以下是将两个多项式 A 和 B 相加得到多项式 C 的步骤。

- 1. 设 A_ptr 和 B_ptr 分别为指向多项式 A 和 B 的指针
- 2. 设 C_ptr = Null，为指向 C 的指针
- 3. while(A_ptr != Null and B_ptr != Null)
   begin
   分配节点，例如 NewTerm

   ```
   NewTerm->link = Null
   if(A_ptr->exponent = B_ptr->exponent)
   then
   begin
   NewTerm->exponent = A_ptr->exponent
   NewTerm->coefficient = A_ptr->coefficient + B_ptr->coefficient
   A_ptr = A_ptr->link
   B_ptr = B_ptr->link
   end
   else if(A_ptr->exponent > B_ptr->exponent)
   begin
   NewTerm->exponent = A_ptr->exponent
   NewTerm->coefficient = A_ptr->coefficient
   A_ptr = A_ptr->link
   end
   else
   begin
   NewTerm->exponent = B_ptr->exponent
   NewTerm->coefficient = B_ptr->coefficient
   B_ptr = B_ptr->link
   end
   attach NewTerm to C
   ```
- 4. while(A_ptr != Null)
   begin
   分配新节点
   NewTerm->link = Null
   NewTerm->exponent = A_ptr->exponent
   NewTerm->coefficient = A_ptr->coefficient
   A_ptr = A_ptr->link
   将 NewTerm 附加到 C
   end
- 5. while(B_ptr != Null)
   begin
   分配新节点
   NewTerm->link = Null
   NewTerm->exponent = B_ptr->exponent
   NewTerm->coefficient = B_ptr->coefficient
   B_ptr = B_ptr->link
   将 NewTerm 附加到 C
   end
- 6. 停止

程序代码 6.15 说明了多项式加法的代码。

```
PROGRAM CODE 6.15
poly Poly :: PolyAdd(Poly F2)
{
  PolyNode *Aptr = Head;
  PolyNode *Bptr = P2.Head;
  Poly C;
  PolyNode *NewTerm;
  while(Aptr != Null && Bptr != Null)
  {
      NewTerm = new PolyNode;
      NewTerm->link = Null;
      if(Aptr->exp == Bptr->exp)
      {
          NewTerm->coef = Aptr->coef + Bptr->coef;
          NewTerm->exp = Aptr->exp;
          C.Append(NewTerm);
          Aptr = Aptr->link;
          Bptr = Bptr->link;
      }
      else if(Aptr->exp > Bptr->exp)
      {
          NewTerm->coef = Aptr->coef;
          NewTerm->exp = Aptr->exp;
          C.Append(NewTerm);
          Aptr = Aptr->link;
      }
      else
      {
          NewTerm->coef = Bptr->coef;
          NewTerm->exp = Bptr->exp;
          C.Append(NewTerm);
          Bptr = Bptr->link;
      }
  } // end of while
  while(Aptr != Null)
  {
      NewTerm = new PolyNode;
      NewTerm->link = Null;
      NewTerm->coef = Aptr->coef;
      NewTerm->exp = Aptr->exp;
      C.Append(NewTerm);
      Aptr = Aptr->link;
  }
  while(Bptr != Null)
  {
      NewTerm = new PolyNode;
      NewTerm->link = Null;
      NewTerm->coef = Bptr->coef;
      NewTerm->exp = Bptr->exp;
      C.Append(NewTerm);
      Bptr = Bptr->link;
  }
  return C;
}
```

## 6.9.3 多项式乘法

设 A = 4x^9 + 3x^6 + 5x^3 + 1 和 B = 3x^6 + x^2 - 2x 为要相乘的两个多项式，结果多项式为 C。让我们重温一下笔算法。多项式 A 乘以 B 的每一项。如果 B 有 n 项，则得到 n 个部分积。最后，将所有这些部分积相加得到结果。

该方法生成的每个部分积长度为 m，其中 m 是多项式 A 的长度。生成、存储这样的 n 个部分积，最后将它们相加得到结果多项式。这里，m 和 n 取决于输入。让我们设计一种更好的方法，不需要生成、存储然后添加所有部分积。因此，更好的解决方案是从多项式 B 中取出一项，将其与多项式 A 的每一项相乘。B 的一项和 A 的一项相乘得到一个结果项。该项可以立即添加到结果多项式 C 中，并重复此过程。

要将残余项添加到多项式 C，需将其与结果多项式 C 的每一项比较，以在多项式 C 的适当位置插入新项。如果找到指数相等的新项，则将该项相加，否则将其插入到结果多项式的适当位置。此过程对 B 的每一项与 A 的每一项重复。主要步骤可列为以下：

- 1. 设 A 和 B 为两个多项式。
- 2. 设 A 中的项数为 M，B 中的项数为 N。
- 3. 设 C 为要计算的结果多项式，即 C = A x B
- 4. 设多项式 B 的第 i 项为 tB_i。对于多项式 B 的每一项 tB_i，重复步骤 5 到 7，其中 i = 1 到 N。
- 5. 设多项式 A 的第 j 项为 tA_j。对于多项式 A 的每一项 tA_j，重复步骤 6 到 7，其中 j = 1 到 M。
- 6. 将 tA_j 和 tB_i 相乘。设新项为 tC_ij = tA_j x tB_i。
- 7. 将 tC_ij 与多项式 C 的每一项比较。如果找到指数相等的项，则将新项 tC_ij 添加到多项式 C 的该项中，否则搜索项 tC_ij 的适当位置并将其插入到多项式 C 中。
- 8. 停止。

程序代码 6.16 显示了两个多项式的乘法。

```
PROGRAM CODE 6.16

poly Poly :: PolyMult(Poly P2)
{
    PolyNode *Aptr = Head;
    PolyNode *Bptr = P2.Head;
    Poly C;
    PolyNode *NewTerm;
    while(Bptr != NULL)
    {
        Aptr = Head;
        while(Aptr != NULL)
        {
            NewTerm = new PolyNode;
            NewTerm->link = Null;
            NewTerm->coef = Aptr->coef * Bptr->coef;
            NewTerm->exp = Aptr->exp + Bptr->exp;
            C.Insert(NewTerm);
            Aptr = Aptr->link;
            cout << "\n C \n";
            C.Display();
        }
        Bptr = Bptr->link;
    }
    return C;
}

void Poly :: Insert(PolyNode *NewTerm)
{
    PolyNode *prev = Head, *Curr = Head;
    if(Head == Null)     // if 1
        Head = Tail = NewTerm;
    else
    {
        Curr = Head;
        while(Curr != Null)
        {
            if(Curr->exp == NewTerm->exp)    //if 2
            {
                Curr->coef += NewTerm->coef;
                break;
            }    else    // else2
            {
                if(Curr->exp < NewTerm->exp)    //if 3
                {
                    if(Curr == Head)    // if 4
                    {
                        NewTerm->link = Head;
                        Head = NewTerm;
                        break;
                    }
                    else    // else 4
                    {
                        prev->link = NewTerm;
                        NewTerm->link = Curr;
                        break;
                    }
                }    // end if 3
            }    // end else 2
            prev = Curr;
            Curr = Curr->link;
        }    // end of while
        if(Curr == Null)    // add at end
        {
            prev->link = NewTerm;
            Tail = NewTerm;
        }    // end of else
}    // end of function

void main()
{
    Poly P1, P2, P3;
    P1.Create();
    P1.Display();
    P2.Create();
    P2.Display();
    P3 = P1.PolyMult(P2);
    P3.Display();
    getch();
}
```

