# wbwTexit

[![npm](https://img.shields.io/npm/v/wbwtexit.svg)](https://www.npmjs.com/package/wbwtexit)
[![license](https://img.shields.io/github/license/wbwblog/wbwtexit.svg)](LICENSE)

`wbwTexit` 是一个可扩展的 LaTeX 解析与 HTML 转换工具，适用于网页和 Node.js 环境。它基于 KaTeX 实现数学公式渲染，并内置常用的文本、数学、环境、变量定义和包扩展支持。

> 主要语言：JavaScript 78.6% ｜ HTML 18.9% ｜ Shell 2.5%

---

## 安装

```bash
npm install wbwtexit
# 或
yarn add wbwtexit
```

## 快速使用

```js
import katex from 'katex';
import { wbwTexit } from 'wbwtexit';

const parser = new wbwTexit();
const latexInput = `
\\section{主要功能演示}
\\textbf{支持粗体文本}\\newline
\\textit{斜体}\\newline
\\underline{下划线}\\newline
\\sout{删除线}\\newline
\\texttt{代码字体}\\newline

\\h1{标题1}
\\section{小节（h2）}
\\subsection{子节（h3）}
\\itemize{
  \\item{条目1}
  \\item{条目2}
}
\\enumerate{
  \\item{一}
  \\item{二}
}
\\p{这是一个段落。}

\\math{f(x) = x^2 + 1}
\\displaymath{f(x) = x^2 + 1}

\\textcolor[red]{彩色文本}
\\fontsize[24px]{更大的字体}

\\href[https://github.com/wbwblog/wbwtexit]{项目地址}
\\includegraphics[width=40px]{/path/to/demo.png}
`;

const html = parser.parseToHTML(latexInput);
console.log(html); // 输出对应的 HTML
```

## Demo 示例

### 1. 渲染基本文本

```js
const parser = new wbwTexit();
console.log(parser.parseToHTML('\\textbf{加粗} 和 \\textit{斜体}'));
```

输出：
```html
<strong>加粗</strong> 和 <em>斜体</em>
```

### 2. 数学公式支持

```js
console.log(parser.parseToHTML('\\math{\\frac{a}{b}}'));
```

输出（KaTeX 渲染片段）：
```html
<span class="katex"> ... </span>
```

### 3. 环境与列表

```js
console.log(parser.parseToHTML(`
\\itemize{
  \\item{苹果}
  \\item{香蕉}
}
`));
```

输出：
```html
<ul><li>苹果</li><li>香蕉</li></ul>
```

### 4. 变量和表达式

```js
parser.parseToHTML('\\set[$x]{"42"}');
parser.parseToHTML('变量：\\var{$x}');
```

输出：
```
变量：42
```

### 5. 其它高级命令

- `\\textcolor[red]{红色字体}`
- `\\fontsize[30px]{超大字}`
- `\\href[https://example.com]{链接文本}`
- `\\includegraphics[width=40px]{/path/to/image.png}`

---

## 扩展包

例如注册 `copytex` 包（内置）：

```js
parser.parseToHTML('\\usepackage[copytex]');
```
会自动注入拷贝 Tex（KaTeX CopyTex 支持）脚本。

---

## 方法与自定义

- 解析字符串： `parser.parseToHTML(str)`
- 注册自定义函数： `parser.registerFunction(name, fn, escape, noargs, force)`

---

## 依赖

- [katex](https://github.com/KaTeX/KaTeX) 用于数学公式渲染

---

## License

[GNU GPLv3.0](./LICENSE)
