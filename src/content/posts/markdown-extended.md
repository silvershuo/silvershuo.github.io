---
title: Markdown 扩展功能
published: 2024-05-01
updated: 2024-11-29
description: '进一步了解 Fuwari 中支持的 Markdown 扩展能力'
image: ''
tags: [示例, Markdown, Fuwari]
category: '示例'
draft: false 
---

## GitHub 仓库卡片
你可以插入链接到 GitHub 仓库的动态卡片。页面加载时，仓库信息会通过 GitHub API 拉取。

::github{repo="Fabrizz/MMM-OnSpotify"}

使用 `::github{repo="<owner>/<repo>"}` 就可以创建 GitHub 仓库卡片。

```markdown
::github{repo="saicaca/fuwari"}
```

## 提示块

目前支持这些提示块类型：`note` `tip` `important` `warning` `caution`

:::note
用于强调即使快速浏览时也值得注意的信息。
:::

:::tip
提供额外提示，帮助读者更顺利地完成操作。
:::

:::important
用于强调对读者真正重要、不可忽略的信息。
:::

:::warning
用于提示存在潜在风险、需要立即留意的内容。
:::

:::caution
用于说明某个操作可能带来的负面后果。
:::

### 基础语法

```markdown
:::note
Highlights information that users should take into account, even when skimming.
:::

:::tip
Optional information to help a user be more successful.
:::
```

### 自定义标题

提示块的标题也可以自定义。

:::note[我的自定义标题]
这是一条带有自定义标题的注记。
:::

```markdown
:::note[我的自定义标题]
这是一条带有自定义标题的注记。
:::
```

### GitHub 语法

> [!TIP]
> 也支持 [GitHub 的提示块语法](https://github.com/orgs/community/discussions/16925)。

```
> [!NOTE]
> 也支持 GitHub 提示块语法。

> [!TIP]
> 也支持 GitHub 提示块语法。
```

### 剧透折叠

你可以在正文中加入剧透折叠，折叠内容同样支持 **Markdown** 语法。

这段内容 :spoiler[被藏起来了 **ayyy**]！

```markdown
这段内容 :spoiler[被藏起来了 **ayyy**]！

```
