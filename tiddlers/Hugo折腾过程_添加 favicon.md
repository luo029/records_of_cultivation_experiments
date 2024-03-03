把 Favicon 图标直接放到 `themes/nostyleplease/static` 目录里

（我同时还放在了`主文件夹/static` 文件里，不过我觉得应该首先使用主题文件夹里的。）

在 `theme/nostyleplease（主题）/layouts/partials/head. html`  文件查找到下面的一行或是直接添加一行：

```html
<link rel="shortcut icon" href="xxx" />
```

然后修改为

```html
<link rel="shortcut icon" href="favicon.ico" />
```
