

```sas
data drugEvents(keep=subject medstdt drug aestdt aedesc sev);
  * define a hash table to hold the subject counter;
  declare hash subjcnt(ordered:'y'); ❶
    subjcnt.definekey('subject');
    subjcnt.definedata('counter');
    subjcnt.definedone();

  declare hash meds(ordered:'y');
    meds.definekey ('subject', 'counter');
    meds.definedata('subject', 'medstdt','drug','counter');
    meds.definedone ();

  * Load the medication data into the hash object;
  do until(almed);
    set advrpt.commed(keep=subject medstdt drug) end=almed; ❷
    * Check subject counter: initialize if not found,
      otherwise increment;
    if subjcnt.find() then counter=1; ❸
    else counter+1; ❹
    * update the subject counter hash table;
    rc=subjcnt.replace(); ❺
    * Use the counter to add this row to the meds hash table;
    rc=meds.add(); ❻
  end;

  do until(alae);
    .... the remainder of the DATA step is unchanged from the previous example ....
```

哈希表 SUBJCNT 包含在任意给定时间已为每位患者读取的药物数量。当遇到更多药物时，COUNTER 变量的值会递增。

- ❶ 声明一个哈希表，用于保存每位患者（SUBJECT）的计数器。键变量是 SUBJECT，唯一的数据变量是 COUNTER。
- ❷ 从药物数据集中读取一条观测。这会将 SUBJECT 的一个值加载到 PDV 中。
- ❸ 当 SUBJECT 的当前值尚未加载到 SUBJCNT 哈希表中时，COUNTER 被初始化为 1。请记住，成功的 FIND 会返回 0 值。这意味着，当 SUBJECT 的当前值是首次遇到该受试者时，表达式 SUBJCNT.FIND() 将为真。当 SUBJCNT.FIND() 成功返回一个值（这不是第一次从药物数据集中读取该 SUBJECT）时，表达式求值为假，并且 COUNTER 会递增 ❹。**无论哪种情况，SUBJCNT.FIND() 都已执行。**
- ❹ 当在哈希表中找到 SUBJECT 的当前值时，会返回 COUNTER 并将其加载到 PDV 中。随后，这个 SUM 语句会使 COUNTER 递增。
- ❺ 更新后的 COUNTER 值会写入哈希表。REPLACE 方法会使该 COUNTER 值覆盖先前的值。
- ❻ 保存药物信息以及更新后的 COUNTER 值。

```sas
data _null_;
  if 0 then set advrpt.demog(keep=clinnum subject lname fname dob); ❶
  * Hash ALL object to hold all the data;
  declare hash all (dataset:'advrpt.demog', ordered:'Y');
    all.definekey ('clinnum','subject');
    all.definedata ('clinnum','subject','lname','fname','dob');
    all.definedone();
  declare hiter hall('all');

  * CLIN object holds one clinic at a time;
  declare hash clin; ❷

  * define the hash for the first clinic; ❸
  clin = _new_ hash(ordered:'Y');
    clin.definekey('clinnum','subject');
    clin.definedata('clinnum','subject','lname','fname','dob');
    clin.definedone();

  * Read the first item from the full list;
  done=hall.first(); ❹
  lastclin = clinnum;

  do until(done);  *loop across all clinics;
    clin.add(); ❺
    done = hall.next(); ❻
    if clinnum ne lastclin then do;
      * This is the first obs for this clinic or the very last obs;
      * write out the data for the previous clinic;
      clin.output(dataset:'clin'||lastclin); ❽
      * Delete the CLIN hash object;
      clin.delete(); ❾
      clin = _new_ hash(ordered:'Y');
        clin.definekey('clinnum','subject');
        clin.definedata('clinnum','subject','lname','fname','dob');
        clin.definedone();
      lastclin=clinnum; ❿
    end;
  end;
  stop;
  run;
```

- ❶ 在 DATA 步的编译阶段，使用 SET 语句为 PDV 上的变量建立属性。这些属性将用于构建由 OUTPUT 方法 ❽ 写出的数据集。
- ❷ 声明 CLIN 哈希对象，它将一次保存一个诊所的数据。
- ❸ 实例化之前声明 ❷ 的哈希对象 CLIN。该对象将保存每个单独诊所的数据。每个诊所将一次一个地加载到 CLIN 对象中 ❺。
- ❹ 使用 ALL 对象的迭代器对象 HALL，从哈希中检索第一个项（值集合）。将这个诊所编号保存在 LASTCLIN 变量中，以便与后续值进行比较。该值用于检测我们何时跨过诊所边界 ❼。
- ❺ PDV 上的当前值会写入 CLIN 对象。对于从 HALL 对象检索到的第一个项，这些值是由 FIRST 方法 ❹ 读取的；否则，这些值是在此 DO UNTIL (DONE) 循环的上一次迭代中由 NEXT 方法 ❻ 读取的。

- 1. 与 SET 语句上的 END= 选项不同（该选项在处理最后一条观测时被赋为真值），NEXT 方法会返回 0，直到它尝试读取超过最后一项。这意味着，在将从 HALL 对象读出的最后一条观测上，DONE 不为真。还需要再执行一次此循环。我们利用这一行为来写出最后一个诊所编号对应的 CLIN 内容。
- 2. 当刚刚检索到的诊所编号与上一个不同（或者当我们读完项）时，我们就知道该将 CLIN 对象的内容写出到一个数据集了。刚刚由 NEXT 方法加载到 PDV 中的值包含来自不同诊所的项，但它们尚未加载到 CLIN 对象中。
- 3. OUTPUT 方法用于将 CLIN 对象的内容（其中只包含一个诊所的行）写入指定的 SAS 数据集。数据集名称包含存储在该数据集中的诊所编号值，并且数据集名称在语句执行期间确定。
- 4. 我们已经写出了特定诊所的哈希对象（CLIN）❸ 的内容，因此我们已用完它。在此示例中，我们将删除 CLIN，然后为下一个诊所重新建立它。由于我们已经声明了 CLIN ❷，因此可以在赋值语句中使用 _NEW_ 关键字重新创建它。我们也可以使用 CLEAR 方法清除 CLIN 对象，而不是删除后再重新建立它。`rc=clin.clear();`（完整 DATA 步请参见本节附带的示例程序）。
- 5. 保存当前诊所编号，以便与下一个检索到的项 ❻ 进行比较 ❼。如果这是最后一项（DONE=1），则没有必要，但代价很小。

## 更多信息

3.3.6 节中的示例还使用嵌套哈希对象创建多个数据子集。

## 另请参阅

Hamilton（2007）非常详细地讨论了这一主题，包括背景和替代方法。

### 3.3.6 引用哈希表的哈希表

命名哈希表的变量所持有的值包含该表特有的信息。

```sas
hashnum = _new_ hash(ordered:'Y');
```

左侧所示的赋值语句实例化哈希表 HASHNUM，当它执行时，一个与该对象关联的唯一值会存储在变量 HASHNUM 中。虽然这个变量存在于 PDV 上，但它并不是传统 DATA 步数值/字符意义上的变量——实际上，这个变量所持有的值就是整个哈希对象。这意味着，只要哈希表变量的值发生变化，我们就可以使用同一个名称实例化多个哈希表。

3.3.5 节中的示例使用两个独立的哈希表将一个数据集拆分为多个依赖于数据的表——每个诊所一个表。该解决方案将特定诊所的数据从主哈希表加载到一个哈希表中。一旦加载完成，该数据子集就会写入一个数据集，并删除或清除相关联的哈希表。此过程要求每条观测经历三次 I/O 传递。

- 1. 从传入数据集中读取它，并加载到主哈希表中。
- 2. 从主哈希表中读取给定诊所的数据，并加载到仅包含该诊所数据的哈希表中。
- 3. 使用 OUTPUT 方法将数据写入新的特定诊所数据集。

