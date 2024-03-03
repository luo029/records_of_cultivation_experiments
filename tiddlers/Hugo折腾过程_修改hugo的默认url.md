以前的博文 url：`https://sicheng.taoooist.org/posts/diary/正月初一`

由于修真日报只放日记，于是删除了 `diary` 文件夹，不再划分文件。

博文 url 变成了：`https://sicheng.taoooist.org/posts/正月初一`

通过修改 `hugo.toml`:


```toml
[permalinks]
  posts = "/:slug/"
  [permalinks.page]
    '/' = '/:slug/'
  [permalinks.term]
    tags = '/:slug/'
```

参照了[小氯的文章](https://yoghurtlee.com/link-modifying-of-twikoo/)和[官方文档](https://gohugo.io/content-management/urls/)，起作用的是 `posts = "/:slug/"`

目前博文 url：`https://sicheng.taoooist.org/正月初一`

