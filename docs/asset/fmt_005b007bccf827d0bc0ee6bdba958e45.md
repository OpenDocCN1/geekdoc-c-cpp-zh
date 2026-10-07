
`cb(node.thenStatement)` ||

`cb(node.elseStatement);`

// .... 其他许多

}

}

```

基本上，它检查 `node.kind` 并根据节点在子节点上调用 `cb`。但请注意，此函数并没有访问所有子节点（例如 `SyntaxKind.SemicolonToken`）。如果你需要所有的 AST，只需调用 Node 的 `.getChildren` 成员函数。例如，这里有一个可以打印节点详细 AST 的函数：

```typescript
function printAllChildren(node: ts.Node, depth = 0) {
  console.log(new Array(depth+1).join('----')), ts.syntaxKindToName(node.kind), node.pos, node.end);
  depth++;
  node.getChildren().forEach(c => printAllChildren(c, depth));
}
```

当我们进一步讨论解析器（parser）时，我们将看到该函数的示例用法。

## AST 提示：SyntaxKind

`SyntaxKind` 被定义为一个常量枚举（const enum），这里有一个示例：

```typescript
export const enum SyntaxKind {
  Unknown,
  EndOfFileToken,
  SingleLineCommentTrivia,
  // ... 更多
}
```

它是一个常量枚举（我们之前涵盖过的一个概念），以便它能被内联（例如 `ts.SyntaxKind.EndOfFileToken` 变为 `1`），这样我们在处理 AST 时就不会产生解引用开销。然而，编译器是使用 `--preserveEnums` 标志编译的，因此该枚举在运行时仍然可用。在 JavaScript 中，如果你需要，可以使用 `ts.SyntaxKind.EndOfFileToken`。此外，你可以使用以下函数将这些枚举成员转换为显示字符串：

```typescript
export function syntaxKindName(kind: ts.SyntaxKind) {
  return (<any>ts).SyntaxKind[kind];
}
```

## Trivia（琐碎元信息）

`Trivia`（因为它们是微不足道的所以被称为此名）代表了源文本中对理解理解代码大部分不重要的部分。例如：空白符、注释，甚至是冲突标记。`Trivia` 不存储在 AST 中（为了保持其轻量级）。但是可以使用几个 `ts.*` API 按需获取。

在展示它们之前，你需要理解以下内容：

### Trivia 所有权

通常情况下：

- 一个 token 拥有它在同一行之后、直到下一个 token 之前的所有 trivia。
- 该行之后的任何注释都与随后的 token 关联联。

对于文件中的开头注释和结尾注释：

- 源文件中的第一个 token 获得所有的初始 trivia。
- 文件中的最后一个 trivia 序列附加在文件结束标记（end-of-file token）上，否则该标记的宽度为零。

### Trivia APIs

对于大多数基础用途，注释是“有趣”的 trivia。属于某个 Node 的注释可以通过以下函数获取：

| 函数 | 描述 |
|---|---|
| `ts.getLeadingCommentRanges` | 给定源文本和在文本中的位置，返回从给定位置之前的第一个换行符到... 之间的注释范围。 |
| `ts.getTrailingCommentRanges` | 给定源文本和在文本中的位置，返回直到给定位置之后的第一个换行符的注释范围。 |

作为示例，源文件中的这部分：

```
debugger;/*hello*/
//bye
/*hi*/function
```

### Token Start/Full Start（标记起始/完全起始）

节点具有所谓的“token start”（标记起始）和“full start”（完全起始）。

- Token Start：更自然的版本，即标记文本在文件中开始的位置。
- Full Start：从扫描器（scanner）自上一个重要标记以来开始的点。

在下面的示例中：

```
debugger;/*hello*/
//bye
/*hi*/
```

对于函数来说，token start 在某处，而 full start 在 `/*hello*/`。注意，full start 甚至包含了本应由上一个节点拥有的 trivia。

## Scanner（扫描器）

TypeScript 扫描器的源代码完全位于 `scanner.ts` 中。扫描器由解析器（Parser）内部控制，将源代码转换为 AST。以下是预期的结果：

```
SourceCode -- scanner --> Token Stream parser --> AST
```

### Parser 使用

`parser.ts` 中创建了一个单例扫描器，以避免重复创建扫描器的开销。该扫描器随后由解析器使用 `initializeState` 函数按需初始化。

以下是解析器中实际代码的简化版本，你可以运行它来演示这一概念：

```typescript
code/compiler/scanner/runScanner.ts
import * as ts from "typescript";

// TypeScript 有一个单例扫描器
const scanner = ts.createScanner(ts.ScriptTarget.Latest, /skipTrivial*/ true);

// 它使用类似于 `initializeState` 的函数初始化
function initializeState(text: string) {
  scanner.setText(text);
  scanner.onError((message: ts.DiagnosticMessage, length: number) => {
    console.error(message);
  });
  scanner.setTarget(ts.ScriptTarget.ES5);
  scanner.setLanguageVariant(ts.LanguageVariant.Standard);
}

// 示例用法
initializeState(
  var foo = 123;
  .trim());

// 开始扫描
var token = scanner.scan();
while (token != ts.SyntaxKind.EndOfFileToken) {
  console.log(ts.formatSyntaxKind(token));
  token = scanner.scan();
}
```

这将输出以下内容：

```
VarKeyword
Identifier
FirstAssignment
FirstLiteralToken
SemicolonToken
```

# 扫描器状态 (Scanner State)

在调用后，扫描器会更新其本地状态（扫描位置、当前标记详细信息等）。扫描器提供了一系列实用函数来获取当前的扫描器状态。在下面的示例中，我们创建了一个扫描器，并使用它来识别标记 以及它们在代码中的位置。

```typescript
code/compiler/scanner/runScannerWithPosition.ts
```

```typescript
// Sample usage
initializeState(
var foo = 123;
.trim());

// Start the scanning
var token = scanner.scan();
while (token != ts.SyntaxKind.EndOfFileToken) {
  let current = ts.formatSyntaxKind(token);
  let tokenStart = scanner.getStartPos();
  token = scanner.scan();
  let tokenEnd = scanner.getStartPos();
  console.log(currentToken, tokenStart, tokenEnd);
}
```

这将输出以下内容：

```
VarKeyword 0 3
Identifier 3 7
FirstAssignment 7 9
FirstLiteralToken 9 13
SemicolonToken 13 14
```

# 独立扫描器 (Standalone scanner)

尽管 TypeScript 解析器内部有一个单例扫描器，但你可以使用 `createScanner` 创建一个独立的扫描器，并使用它的 `setText` / `setTextPos` 来扫描文件中的不同点以供玩玩。

# 解析器 (Parser)

TypeScript 解析器的源码完全位于 `parser.ts` 中。扫描器由解析器内部控制，用于将源代码转换为 AST（抽象语法树）。以下是预期结果的概述。

```
SourceCode -- --> Token Stream -- parser --> AST
```

解析器是以单例形式实现的（与扫描器的原因类似，如果可以重新初始化，我们就不希望重新创建它）。它实际上被实现为 `Parser` 命名空间，其中包含了解析器的状态变量以及一个单例扫描器。如前所述，它包含一个 `const scanner`。解析器函数管理着这个扫描器。

# 程序调用 (Usage by program)

解析器由 `Program` 直接驱动（实际上间接是由我们之前提到的 `CompilerHost` 驱动的）。基本上，这是简化的调用堆栈：

```
Program -> CompilerHost.getSourceFile -> (global function parser.ts).createSourceFile -> Parser.parseSourceFile
```

`parseSourceFile` 不仅为解析器准备状态，还通过调用 `initState` 为扫描器准备状态。然后它使用 `parseSourceFileWorker` 解析源文件。

# 示例用法 (Sample Usage)

在我们深入研究解析器内部之前，这里有一个示例代码，使用 TypeScript 解析器获取源文件的 AST（使用 `ts.createSourceFile`），然后将其打印。

```typescript
code/compiler/parser/runParser.ts
```

```typescript
import * as ts from "typescript";
function printAllChildren(node: ts.Node, depth = 0) {
  console.log(new Array(depth + 1).join('-'), ts.formatSyntaxKind(node.kind), node.pos, node.end);
  depth++;
  node.getChildren().forEach(c=> printAllChildren(c, depth));
}
var sourceCode = `
var foo = 123;
.trim();
var sourceFile = ts.createSourceFile('foo.ts', sourceCode, ts.ScriptTarget.ES5, true);
printAllChildren(sourceFile);
```

这将输出以下内容：

```
SourceFile 0 14
--- SyntaxList 0 14
---- VariableDeclarationList 0 14
      ------ VariableDeclaration 0 13
      ------ VarKeyword 0 3
      ------ SyntaxList 3 13
        -------- Identifier 3 7
        ---------- FirstAssignment 7 9
        ---------- FirstLiteralToken 9 13
    ---- SemicolonToken 13 14
--- EndFileToken 14 14
```

如果你把头向左倾，这看起来像是一棵右右的树。

# 解析器函数 (Parser Functions)

如所述，`parseSourceFile` 设置了初始状态并将工作交给 `parseSourceFileWorker`。

# parseFileWorker

从创建 `SourceFile` AST 节点开始。然后从 `parseStatements` 函数开始解析源代码。完成后，它返回 `SourceFile` 节点。

# parseStatements

解析器中最重要的函数之一是 `parseStatements`。它根据 `node.kind`（类型为 `SyntaxKind`）进行切换并将工作委托给相应的 `bindFoo` 函数（定义在 `binder.ts` 中）。

# 节点创建 (Node creation)

绑定的工作单元是 `SourceFile`。`binder.ts` 由 `checker` 驱动。

# Binder 函数 (Binder function)

两个关键的绑定函数是 `bindSourceFile` 和 `mergeSymbolTable`。接下来我们将查看它们。

# bindSourceFile

基本上检查 `file.locals` 是否定义，如果没有，则交给（本地函数）`bind`。

注意：`locals` 定义在 `Node` 上，类型为 `SymbolTable`。注意 `SourceFile` 也是一个 `Node`（实际上是根节点）。

# bind

`bind` 接收任何 `Node`（不仅仅是 `SourceFile`）。它执行的第一件事是赋值 `node.parent`（如果 parent 变量已设置……这是绑定在 `bindchildren` 的处理过程中完成的），然后交给执行重体工作的 `bindworker`。最后，它调用 `bindChildren`（一个简单的函数，它在在函数变量中存储绑定状态，然后对每个孩子调用 `bind`，并恢复绑定状态）。

# binder

此函数根据 `node.kind`（类型为 `SyntaxKind`）进行切换并将工作委托给相应的 `bindFoo` 函数（定义在 `binder.ts` 中）。例如，如果节点是 `SourceFile`，它会调用（最终且仅当它是外部文件模块时）`bindAnonymousDeclaration`。

# Symbol

`bindFoo` 函数之间有一些共同模式，以及这些函数使用的一些实用函数。一个几乎总是使用的的是 `createSymbol` 函数。它完整地呈现如下所示：

```typescript
function createSymbol(flags: SymbolFlags, name: string): Symbol {
    symbolCount++;
    return new Symbol(flags, name);
}
```

如你所见，它仅仅是保持 `symbolCount`（`bindSourceFile` 的局部变量）更新，并使用指定的参数创建符号。

# 符号与声明

节点与符号之间的链接通过几个函数完成。其中用于将 `SourceFile` 绑定到源文件 `Symbol`（针对外部模块）的函数是 `addDeclarationToSymbol`。

注意：外部模块文件的 `Symbol` 设置为 `flags : SymbolFlags.ValueModule` 和 `name: '' + removeFileExtension(file.fileName) + ''`。

```typescript
function addDeclarationToSymbol(symbol: Symbol, node: Declaration, symbolFlags: SymbolFlags) {
    symbol.flags |= symbolFlags;
    node.symbol = symbol;
    if (!symbol.declarations) {
        symbol.declarations = [];
    }
    symbol.declarations.push(node);
    if (symbolFlags & SymbolFlags.HasExports && !symbol.exports) {
        symbol.exports = {};
    }
    if (symbolFlags & SymbolFlags.HasMembers && !symbol.members) {
        symbol.members = {};
    }
    if (symbolFlags & SymbolFlags.Value && !symbol.valueDeclaration) {
        symbol.valueDeclaration = node;
    }
}
```
