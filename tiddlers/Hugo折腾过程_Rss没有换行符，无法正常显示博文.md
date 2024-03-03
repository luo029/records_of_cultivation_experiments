### 前言

默认 rss 模板中，博文没有换行符 `<p>`。

例子：


```xml
<description> 早晚课，早晚功，咕咕。 折腾 tw，无甚事。 话说，天台今天过元宵节？ 应该吃汤圆吧。 午斋。 就酱~ 甲辰正月十四 嗣檙 于桐柏宫</description>
```

此时如果通过 rss 订阅的话，就会发现正文无法换行，堆叠在一块。

修改后：


```xml
<description><p>早晚课，早晚功，咕咕。</p> <p>折腾 tw，无甚事。</p> <p>话说，天台今天过元宵节？应该吃汤圆吧。</p> <p><img src="https://cdn.jsdelivr.net/gh/luo029/blogimage@main/24%200223%202146%2056.png" alt="image.png"></p> <p>午斋。</p> <p>就酱~</p> <p>甲辰正月十四</p> <p>嗣檙 于桐柏宫</p></description>
```

有了换行符，同时博文内容正常显示（博文里有外部链接图片的话，在默认模板里似乎无法显示。）


博客 Rss 查看：`域名/index.xml`

### 解决方案

在 `themes\nostyleplease (主题名）\layouts\_default` 中添加 `rss.xml` :

```xml
{{- /* Generate RSS v2 with full page content. */ -}}
{{- /* Upstream Hugo bug - RSS dates can be in future: https://github.com/gohugoio/hugo/issues/3918 */ -}}
{{- $page_context := cond .IsHome site . -}}
{{- $pages := $page_context.RegularPages -}}
{{- $limit := site.Config.Services.RSS.Limit -}}
{{- if ge $limit 1 -}}
  {{- $pages = $pages | first $limit -}}
{{- end -}}
{{- printf "<?xml version=\"1.0\" encoding=\"utf-8\" standalone=\"yes\" ?>" | safeHTML }}
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <title>{{ if ne .Title site.Title }}{{ with .Title }}{{.}} | {{ end }}{{end}}{{ site.Title }}</title>
    <link>{{ .Permalink }}</link>
    {{- with .OutputFormats.Get "RSS" }}
      {{ printf "<atom:link href=%q rel=\"self\" type=%q />" .Permalink .MediaType | safeHTML }}
    {{ end -}}
    <description>{{ .Title | default site.Title }}</description>
    <generator>Source Themes Academic (https://sourcethemes.com/academic/)</generator>
    {{- with site.LanguageCode }}<language>{{.}}</language>{{end -}}
    {{- with site.Copyright }}<copyright>{{ replace (replace . "{year}" now.Year) "&copy;" "©" | plainify }}</copyright>{{end -}}
    {{- if not .Date.IsZero }}<lastBuildDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</lastBuildDate>{{ end -}}
    {{- if .Scratch.Get "og_image" }}
    <image>
      <url>{{ .Scratch.Get "og_image" }}</url>
      <title>{{ .Title | default site.Title }}</title>
      <link>{{ .Permalink }}</link>
    </image>
    {{end -}}
    {{ range $pages }}
    <item>
      <title>{{ .Title }}</title>
      <link>{{ .Permalink }}</link>
      <pubDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</pubDate>
      <guid>{{ .Permalink }}</guid>
      <description>{{ .Content | html }}</description>
    </item>
    {{ end }}
  </channel>
</rss>
```
