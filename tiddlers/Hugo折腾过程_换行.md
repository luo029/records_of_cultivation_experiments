	时间：2024.2.10/2.14
### 问题：
源码模式：
```powershell
Hello
World
```
渲染后（并未完成换行）：
```powershell
Hello World
```
### 原因
根据 [Markdown Syntax](https://daringfireball.net/projects/markdown/syntax#p) 文档，当从源码输出为 HTML 时，换行符（软换行）不会被转换为 `<br />` （硬换行），如果要插入硬换行，你需要在行尾输入两个（或更多）空格。

根据 [GitHub Flavored Markdown Spec](https://github.github.com/gfm/#hard-line-breaks) 文档，要插入硬换行，你还可以在行尾输入 \ 或者直接输入 `<br />` 。

### 解决  
Hugo 的硬换行默认关闭。
https://gohugo.io/getting-started/configuration-markup/#configure-markup

在 `hugo.toml` 中添加
```powershell
[markup]
  [markup.goldmark]
    [markup.goldmark.renderer]
      hardWraps = true
```

或者：

使用 typora 编辑，换行时会自动空出一行。

使用 obsidian 编辑，使用插件 easy typing，插件的配置中，有一个“一次回车产生两个换行符”的选项，打开即与 typora 相同。