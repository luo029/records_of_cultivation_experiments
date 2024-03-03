## 问题

用[tidgi](https://tidgi.fun)创建wiki，删除`itonnote`插件，上传到github自动部署，网页默认语言为英文，不是tidgi里设置的默认语言

## 原因

`language.tid` 没有上传

## 解决

删除`.gitignore` 里的`tiddlers/$__language.tid`