# LISTING 7-27 Checking that each BST node has only one child

```
let (|Diff||_|) (a, b) =
  if (a * b < 0) || (a * b == 0 && b < 0) then Some
else None

let checkOneChild(preorder : int list) =
  seq {
    for i=0; i < preorder.Length - 2 do
    let a = preorder[i]-preorder[i + 1];
    let b = preorder[i]-preorder[preorder.Length - 1];
    yield (a, b)
  }
|> Seq.forall (fun (a, b) -> match a, b with
    | Diff _ -> false
    | _ -> true)

let list = [20; 10; 11; 13; 12];
```

checkOneChild list

```
C# version
bool checkOneChild(int[] preorder)
{
  for (int i = 0; i < preorder.Length - 2; i++)
  {
      int a = preorder[i]-preorder[i + 1];
      int b = preorder[i]-preorder[preorder.Length - 1];
      if (a * b < 0) || (a * b == 0 && b < 0 )
      {
          return false;
      }
  }
  return true;
}
```

> Note The partial active pattern is used to categorize data. If (a, b) are different, the function will return false.