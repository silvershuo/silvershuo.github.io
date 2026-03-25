---
title: Expressive Code 示例
published: 2024-04-10
description: 演示在 Markdown 中使用 Expressive Code 后，代码块会呈现成什么样。
tags: [Markdown, 博客, 示例]
category: 示例
draft: false
---

这篇文章会演示使用 [Expressive Code](https://expressive-code.com/) 后代码块的展示效果。下面的示例主要参考了官方文档，想了解更多细节也可以直接去看原文。

## Expressive Code

### 语法高亮

[语法高亮](https://expressive-code.com/key-features/syntax-highlighting/)

#### 常规语法高亮

```js
console.log('这段代码启用了语法高亮！')
```

#### 渲染 ANSI 转义序列

```ansi
ANSI 颜色：
- 常规:  颜色示例
- 粗体:  颜色示例
- 变暗:  颜色示例

256 色示例（展示 160-177 号颜色）：
160 161 162 163 164 165
166 167 168 169 170 171
172 173 174 175 176 177

完整 RGB 颜色：
ForestGreen - RGB(34, 139, 34)

文本样式：Bold Dimmed Italic Underline
```

### 编辑器与终端框架

[编辑器与终端框架](https://expressive-code.com/key-features/frames/)

#### 代码编辑器框架

```js title="my-test-file.js"
console.log('title 属性示例')
```

---

```html
<!-- src/content/index.html -->
<div>文件名注释示例</div>
```

#### 终端框架

```bash
echo "这个终端框架没有标题"
```

---

```powershell title="PowerShell 终端示例"
Write-Output "这个示例有标题！"
```

#### 覆盖默认框架类型

```sh frame="none"
echo "看，没有外框了！"
```

---

```ps frame="code" title="PowerShell Profile.ps1"
# 如果不手动覆盖，这里原本会显示成终端框架
function Watch-Tail { Get-Content -Tail 20 -Wait $args }
New-Alias tail Watch-Tail
```

### 文本与行标记

[文本与行标记](https://expressive-code.com/key-features/text-markers/)

#### 标记整行与行范围

```js {1, 4, 7-8}
// 第 1 行 - 通过行号命中
// 第 2 行
// 第 3 行
// 第 4 行 - 通过行号命中
// 第 5 行
// 第 6 行
// 第 7 行 - 通过区间 "7-8" 命中
// 第 8 行 - 通过区间 "7-8" 命中
```

#### 选择行标记类型（mark、ins、del）

```js title="line-markers.js" del={2} ins={3-4} {6}
function demo() {
  console.log('这一行会被标记为删除')
  // 这一行和下一行会被标记为新增
  console.log('这是第二行新增内容')

  return '这一行使用默认的中性标记类型'
}
```

#### 为行标记添加标签

```jsx {"1":5} del={"2":7-8} ins={"3":10-12}
// labeled-line-markers.jsx
<button
  role="button"
  {...props}
  value={value}
  className={buttonClassName}
  disabled={disabled}
  active={active}
>
  {children &&
    !active &&
    (typeof children === 'string' ? <span>{children}</span> : children)}
</button>
```

#### 为长标签单独占行

```jsx {"1. 在这里传入 value 属性：":5-6} del={"2. 删除 disabled 和 active 状态：":8-10} ins={"3. 新增这段代码，让 children 渲染在按钮内部：":12-15}
// labeled-line-markers.jsx
<button
  role="button"
  {...props}

  value={value}
  className={buttonClassName}

  disabled={disabled}
  active={active}
>

  {children &&
    !active &&
    (typeof children === 'string' ? <span>{children}</span> : children)}
</button>
```

#### 使用类似 diff 的语法

```diff
+这一行会被标记为新增
-这一行会被标记为删除
这是一行普通内容
```

---

```diff
--- a/README.md
+++ b/README.md
@@ -1,3 +1,4 @@
+这是一份真正的 diff 文件
-所有内容都会保持原样
 不会额外移除任何空白字符
```

#### 将语法高亮与 diff 风格语法结合使用

```diff lang="js"
  function thisIsJavaScript() {
    // 整个代码块会按 JavaScript 做语法高亮，
    // 同时仍然可以继续使用 diff 标记！
-   console.log('将被移除的旧代码')
+   console.log('全新的闪亮代码！')
  }
```

#### 标记行内的局部文本

```js "指定文字"
function demo() {
  // 标记行内出现的指定文字
  return '同一段指定文字也支持匹配多次';
}
```

#### 正则表达式

```ts /ye[sp]/
console.log('yes 和 yep 这两个词都会被标记。')
```

#### 转义正斜杠

```sh /\/ho.*\//
echo "Test" > /home/test.txt
```

#### 选择行内标记类型（mark、ins、del）

```js "return true;" ins="inserted" del="deleted"
function demo() {
  console.log('这里分别演示了新增和删除标记类型');
  // return 这一行使用的是默认标记类型
  return true;
}
```

### 自动换行

[自动换行](https://expressive-code.com/key-features/word-wrap/)

#### 为单个代码块配置换行

```js wrap
// 启用换行的示例
function getLongString() {
  return '这是一段很长的字符串，如果容器不是特别宽，它大概率放不下，需要自动换行'
}
```

---

```js wrap=false
// 禁用换行的示例
function getLongString() {
  return '这是一段很长的字符串，如果容器不是特别宽，它大概率放不下，需要自动换行'
}
```

#### 配置换行后文本的缩进

```js wrap preserveIndent
// preserveIndent 示例（默认开启）
function getLongString() {
  return '这是一段很长的字符串，如果容器不是特别宽，它大概率放不下，需要自动换行'
}
```

---

```js wrap preserveIndent=false
// preserveIndent=false 示例
function getLongString() {
  return '这是一段很长的字符串，如果容器不是特别宽，它大概率放不下，需要自动换行'
}
```

## 可折叠区块

[可折叠区块](https://expressive-code.com/plugins/collapsible-sections/)

```js collapse={1-5, 12-14, 21-24}
// 这一大段样板初始化代码会默认折叠
import { someBoilerplateEngine } from '@example/some-boilerplate'
import { evenMoreBoilerplate } from '@example/even-more-boilerplate'

const engine = someBoilerplateEngine(evenMoreBoilerplate())

// 这部分代码会默认保持展开
engine.doSomething(1, 2, 3, calcFn)

function calcFn() {
  // 一个代码块里也可以有多个折叠区段
  const a = 1
  const b = 2
  const c = a + b

  // 这一行会保持可见
  console.log(`计算结果：${a} + ${b} = ${c}`)
  return c
}

// 从这里到代码块结束会再次被折叠
engine.closeConnection()
engine.freeMemory()
engine.shutdown({ reason: '示例样板代码结束' })
```

## 行号

[行号](https://expressive-code.com/plugins/line-numbers/)

### 为单个代码块显示行号

```js showLineNumbers
// 这个代码块会显示行号
console.log('这里是第 2 行！')
console.log('我现在位于第 3 行')
```

---

```js showLineNumbers=false
// 这个代码块禁用了行号
console.log('你好？')
console.log('请问你知道我现在在第几行吗？')
```

### 修改起始行号

```js showLineNumbers startLineNumber=5
console.log('这里是第 5 行！')
console.log('我现在位于第 6 行')
```
