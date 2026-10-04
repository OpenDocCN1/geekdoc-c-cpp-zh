

# 第 2 章 面向对象语言的依赖图与切片

通过传递给 $c$ 处的 $m'$ 的变量。由于我们使用了 GRef 和 GMod 而不是 IRef 和 IMod，因此需要对全局副作用进行不动点迭代，这些副作用也包括被调用方法的副作用。

图 2.16 显示了将这些定义应用于我们在 2.5.1 节中确定的运行示例的局部副作用 $IRef \subseteq GRef$ 和 $IMod \subseteq GMod$ 的结果：$CMod \supset \{(B.init, new(A)), (B.init, new(A), n.2)\}$ 和 $CRef \supset \{(foo(), bar(a))\}$。注意隐式变量 $Ain$ 已重命名为实际参数 $a$ 的名称。此外，图中对应的节点已通过参数输入和输出边连接，留下了 $IMod(Ain)$ 的根节点。这种异常是 Java 的值传递参数传递方案，它不会将形式参数的变化传回给其调用者。

方法顶点包含参数树，对于 GRef 中的每个位置都有一个形式输入（formal-in），对于 GMod 中的每个位置都有一个形式输出（formal-out）节点。对于虚拟方法，这意味着并不是每个形式节点恰恰对应一个节点（CRef/GRef）：虚拟方法的不同（重）定义可能会改变参数的不同字段集。因此，CRef/GMod 中的每棵树都是此处呈现的所有对应树的并集。

现在，被调用方法的副作用在它们所在的位置是可用的，它们可能代表包含调用的方法的副作用。例如，$B$ 构造函数中的 $a.x$ 也是该方法的副作用。因此，我们需要另一个函数 $bind_{m,c}(Param(m) \cup Param(m) \cup IRef(m))$，它对于方法 $m$ 中方法 $c$ 的给定参数，返回对齐的 $IRef(m)$ 中的形式参数或位置：

```
$bind_{m,c}(x) := \{y \in Param(m) \cup IRef_{\sim}(m) : myAlias(x,y)\}$ (2.8)
```

同样，该定义扩展到了参数集。在我们的示例程序中，$B.init,new(A) = \{(this.a)\}$ 且 $bind_{foo(),bar(a)}(a) = \{this.a\}$。对于两个位置 $y$ 和 $z$，追加函数 $@$ 返回 $y$ 和 $z$ 的访问路径连接后的连接位置：

## **定义 2.19 (Append)。** 对于两个位置 $y = v.f1...fn_n$ 和 $z = w.g1...gm_m$，如果 may-alias(y,w)，则连接后的 $@z = v.f1...fn_n.w.g1...gm_m$。

现在，被调用方法的全局副作用 [Ban79] 可以包含在方法的参数中：

```
$GRef = \{m, t) | t \in IRef_{\sim}(m) : t = y@z : c \in Calls(m) : z \in CRef(m, c) \wedge y \in bind_{m,c}(root(z))\}$ (2.9)
```

```
$GMod = \{m, t) | t \in IMod_{\sim}(m) : t = y@z : c \in Calls(m) : z \in CMod(m, c) \wedge y \in bind_{m,c}(root(z))\}$ (2.10)
```

## 2.5. 过程数据流分析

![](img/27c6595637bae6b27613772d7079f8a2_66_0.png)

图 2.16：类 B 的中间 SDG，过程间 CRef/CMod 传播的第一次迭代。

![](img/27c6595637bae6b27613772d7079f8a2_66_1.png)

图 2.17：类 B 的中间 SDG：GRef/GMod 的第一次迭代。

同样，我们定义函数 $GRef(m) = \{t | (m,t) \in GRef\}$ 和 $GMod(m) = \{t | (m,t) \in GMod\}$。CRef 和 GRef 是相互递归的，最小不动点给出了所需的解。同样，考虑 GRef 和 GMod 定义中 $\sim$ 关系的代表元是足够的，因为保证了这个不动点的存在。

考虑我们的运行示例，图 2.17 显示了 GRef 和 GMod 计算的第一次迭代：$GMod \supseteq \{(B.init,this), (B.init,this,a), (B.init,this,x)\}$ 和 $GRef \supseteq \{(foo(this),this), (foo(this),this,a), (foo(this),this,x)\}$。

在第二次迭代后，CRef CMod 包含图 2.15 所示的位置：$\{(main(i), foo(b), b.a), (main(i), newB(b), b.x)\}$ 和 $CRef \supseteq \{(main(i), foo(l), b.a), (main(i), (main), b.x)\}$。由于 $bound\_foo$ 为空（main 的参数为形式参数），不动点迭代在此结束。

### 2.5.3 数据依赖

当所有全局副作用都计算完毕后，字段的数据依赖根据定义 2.18 确定。GRef 被视为对应方法的入口 Def。

![](img/27c6595637bae6b27613772d7079f8a2_67_0.png)

图 18：类 B 的 SDG：CRef/CMod 传播后的不动点。

![](img/27c6595637bae6b27613772d7079f8a2_67_1.png)

图 19：类 B 的 SDG：包含数据依赖（但不包含摘要边）。

### 2.5.4. 过程数据流分析

相反，CRef 的元素插入到调用节点的 Ref 和 CMod 中 [HR90]。标准过程内到达定义集仅在 must-alias 关系成立时填充。数据依赖随后使用 2.18 确定。

在我们的运行示例中，图 19 显示了测试结果：在 A.init 中，定义 $x$ 到达了节点，我们得到了该定义与 GMod 中使用之间的依赖。同样，合成定义 bar(bar) 到达了返回语句并产生了数据依赖。在 main 中，new() 到达了 CRef(main) 的合成使用，因此这些位置之间插入了数据依赖。

**对象树的摘要边**

对于带有对象树的摘要边，为了避免爆炸至关重要：如果实际参数的摘要边指向 $n$，那么父节点(s) 也会指向 $n$。但这些边是冗余的，可以始终跟随摘要边到父节点，因此切片结果将相同。

之前的工作 [RYS88, B89, PS91] 已证明了多个切片维度（过程间切片和堆对象，见第 36 页）。由于过程间切片与堆对象的结合尚未明确证明，我们关注堆对象的过程间数据依赖正确性。因此，为了证明我们算法的正确性，需要证明所有动态数据依赖都被静态数据依赖所近似，即当语句在执行中定义了一个字段值并在另一个语句中使用它时，SDG 的对应节点之间存在依赖链。对于方法调用，我们假设在动态执行中，被调用方法的最后一个语句是赋值给返回结果变量的调用。随后，我们检测到带有 label(e) 的 SDG 依赖类型，例如，$label(x->y) = correspondingCall(n)$ 表示创建语句栈的调用，$n$ 通常是一个返回语句。

**定理 2.2（对象树的正确性）。** 对于所有根据 2.5 节构建 SDG 的程序运行 $p$，如果执行 $E$ 包含路径 $P = (p_1,\dots,p_n)$，其中 $p_i$ 定义了内存单元 $mem$ 且 $p_n$ 读取了 $mem$，$p_1 = correspondingCall(n)$ 且 $p_i$ 和 $p_n$ 都由于参数传递是字段赋值，或 $p_i$ 是普通的字段赋值$^9$（不假设此赋值构成了一个过程间语句），并且对于 $\forall p_i \in \{p_2, \dots, p_n\}$，$p_i$ 都不是内存的普通字段赋值，那么在 $G$ 中存在 $p$ 使得 $S=(p_1=s_1, \dots, s_m=p_n)$，其中 label$(s_i, s_{i+1}) \in [DD, PI, PO]$。

证明。证明是对执行轨迹 $P$ 中过程间语句数量 $q$ 的归纳。

**基础情况：$q=0$（过程内情况）** 我们有 $P=(p_1,\dots,p_n)$ 是 $E$ 的子序列，其中 $p_1$ 定义了内存单元 $mem$ 且 $p_n$ 读取了 $mem$，因此对于字段 $f，$p_1 \in Def(f)$ 且 $p_n \in Ref(f)$且 may-aliases($base(p_1), base(p_n)$)。由于 $p_i \in \{p_2, \dots, p_n\}$ 的名称在执行中细化了内存 $mem$p_1$ 在 CFG 中到达 $p_n$，且 points-to($p_1$) $\cap$ points-to($p_n$) $\neq \emptyset$。因此适用定义 2.18，我们得到了

**归纳步骤：$q \rightarrow q+1$**

$P$ 中最后一个过程间语句 $p_i$ 是一个调用：

```
$ \dots p_n$
```

$p_1 \dots$

- a) Java 中的普通字段访问语句只能访问内存$^{10}$，所以我们知道存在访问路径 $A=\langle f_1, \dots, f_d \rangle$，通过它 $p_n$ 获取了对 $mem$ 的访问。根据等式 (2.3），A' \in IRef(method(n))$ 使得访问路径 $A'$ 和 $A$ 的长度都是 $mem$ 的别名。
 b) 对于调用语句 $p_n$ 的实际参数 $A=\langle act, f_1, \dots, f_n \rangle，$A \in Ref(method(n))$，存在一个参数形式使得访问路径 $A'=\langle f_1, \dots, f_g \rangle @A$ 是 $mem$ 的别名，根据等式 (2.9)。
 c) 如果 $p_i$ 是返回语句，则 $p_n$ 处的使用 $A=\langle f_1, \dots, f_d \rangle$ 必须在 $GMod(method(n))$ 中。根据方程 (2.9)，我们得到 $A' \in Ref(method(n))$。

