---
title: Fuwari 使用小指南
published: 2024-04-01
description: "这篇文章简单介绍如何使用这个博客模板。"
image: "./cover.jpeg"
tags: ["Fuwari", "博客", "自定义"]
category: 指南
draft: false
---

> 封面图来源：[Source](https://image.civitai.com/xG1nkqKTMzGDvpLrqFT7WA/208fc754-890d-4adb-9753-2c963332675d/width=2048/01651-1456859105-(colour_1.5),girl,_Blue,yellow,green,cyan,purple,red,pink,_best,8k,UHD,masterpiece,male%20focus,%201boy,gloves,%20ponytail,%20long%20hair,.jpeg)

这个博客模板基于 [Astro](https://astro.build/) 构建。如果这篇指南没有提到某些内容，通常都可以在 [Astro 文档](https://docs.astro.build/) 里找到答案。

## 文章 Frontmatter

```yaml
---
title: 我的第一篇博客文章
published: 2023-09-09
description: 这是我新的 Astro 博客的第一篇文章。
image: ./cover.jpg
tags: [Foo, Bar]
category: 前端
draft: false
---
```

| 属性 | 说明 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title` | 文章标题。 |
| `published` | 文章发布时间。 |
| `description` | 文章的简短描述，会显示在首页列表中。 |
| `image` | 文章封面图路径。<br/>1. 以 `http://` 或 `https://` 开头：使用网络图片<br/>2. 以 `/` 开头：使用 `public` 目录中的图片<br/>3. 不带这些前缀：相对于当前 Markdown 文件的相对路径 |
| `tags` | 文章标签。 |
| `category` | 文章分类。 |
| `draft` | 如果这篇文章仍是草稿，就不会对访客显示。 |

## 文章文件放在哪里

你的文章文件应该放在 `src/content/posts/` 目录下。你也可以创建子目录，以便更好地整理文章和相关资源。

```
src/content/posts/
├── post-1.md
└── post-2/
    ├── cover.png
    └── index.md
```
