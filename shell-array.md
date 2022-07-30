---
date: 20220730
keyword: shell
---

# Shell Array

Shell array is defined as:

```shell
array=(1 2 3 4 5)
```

An element in shell array can be accessed by index, like:

```shell
echo ${array[0]} # 1
```

All elements can be accessed like:

```shell
echo ${array[*]} # 1 2 3 4 5
# or
echo ${array[@]} # 1 2 3 4 5
```

An example to install all given vscode extensions:

```shell
extensions=(
  "ms-vscode.cpptools"
  "ms-vscode.csharp"
  "ms-vscode.go"
  "ms-vscode.java"
  "ms-vscode.python"
  "ms-vscode.rust"
  "ms-vscode.typescript"
)
for extension in ${extensions[@]}; do
  code --install-extension $extension
done
```
