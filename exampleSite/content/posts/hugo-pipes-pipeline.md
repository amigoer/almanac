---
title: "Hugo Pipes：把 build chain 收进一个 hugo 命令"
date: 2026-04-15
summary: "为什么这个主题没有 webpack / vite / parcel —— Hugo Pipes + PostCSS 一条命令搞定 CSS 和 JS。"
tags: ["Hugo", "构建", "前端"]
categories: ["技术"]
---

## 静态站不需要打包器

Hugo 自带 `resources.Get` + `css.PostCSS` + `js.Build` + `minify` + `fingerprint`，这套 pipeline 加起来够用了：

```go-html-template
{{ with resources.Get "css/main.css" }}
  {{ $opts := dict "inlineImports" true }}
  {{ $css := . | css.PostCSS $opts | minify | fingerprint }}
  <link rel="stylesheet" href="{{ $css.RelPermalink }}" integrity="{{ $css.Data.Integrity }}">
{{ end }}
```

这一段做了：

1. 读 `assets/css/main.css`
2. 走 PostCSS（处理 `@tailwindcss/postcss` 和 `autoprefixer`）
3. minify
4. 加 hash fingerprint + SRI integrity 头

不需要 dev server，不需要 manifest 解析。

## 唯一的 Node 依赖

只剩 `postcss-cli` 和 `@tailwindcss/postcss` —— 因为 Hugo Pipes 需要 PostCSS 把 Tailwind 编译出来。如果哪天 Hugo 内置了 Tailwind，连 Node 都不用装。

## Alpine.js 走 CDN

交互那一点点用 Alpine.js，直接 `<script defer src="https://unpkg.com/alpinejs">`，不进 build chain。这条线退化得可以。
