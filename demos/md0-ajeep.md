---
title: markdown初步
author: ajeep
language: markdown
columns: 3
theme: blue
border: thin
corner: 0
publish: yes
---

# metadata(元数据)

metadata是在md文件最前面用两行\-\-\-扩起来，定义一些元数据供渲染器、转换器使用。如：

```
---
title: 文件标题
subtitle: 副标题
author：作者
date: 日期
---

# 标题

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

# 列表

|无序列表|有序列表|混用|序号格式|
|-|-|-|-|
|- 红<br>- 绿<br>    -深绿<br>    - 浅绿<br>-蓝|1. 红<br>1. 绿<br>    1. 深绿<br>    1. 浅绿<br>1. 蓝|1. 红<br>1. 绿<br>    - 深绿<br>    - 浅绿<br>1. 蓝|1. 红<br>1. 绿<br>    1) 深绿<br>    1) 浅绿<br>        a. 泛绿<br>        b. 显绿<br>1. 蓝|

列表层级靠4个空格分级，再下一级就是8个空格，类推

# 强调

```
*斜体*，_斜体_。
**加粗**，__加粗__。
***斜体加粗***，___斜体加粗___。
~~删除文字~~ 
```

下面两种仅pandoc支持：

```
[pandoc下划线]{.underline}
[pandoc Small Capital text]{.smallcaps}
```

# 图片和链接

插图和链接可以使用URL，也可以使用本地路径(相对路径和绝对路径都行)。

```
- 链接：[markdown进阶](md1.md)
- 图片：![markdown图标](https://markdown.com.cn/hero.png){width=30%}
- 引用方式: ![markdown图标][mdlogo]
```

引用方式在后面统一定义、可以多次引用，正文部分更干净，如本例：

```
[mdlogo]: https://markdown.com.cn/hero.png
```

# 表格

```
Table: 表格标题

| 第一列台头 | 左对齐 | 中对齐 | 右对齐 |
| -------- |:----- |: --- :| -----:|
|   内 容   | 内 容  |  内 容 | 转pdf有bug？一行内容不到72个字符不折行。绕过的方法是增加参数--columns=10设置一个很小的数。 |
|   内容    | *内容* | **内容** | $e^{i\pi}+1=0$ |
```

"Table"可省略、只以:开头，放在表前表后都可

# 公式

独立公式用2个 \$ 扩起来，如质能方程：

$$
E=mc^2
$$

行内公式用1个 \$ 扩起来。例如欧拉公式：$e^{i\pi}+1=0$。

# Fenced Code Block (代码块)

独立代码块前后用3个\`扩起来，即\`\`\`：

~~~
```
ls -al
```
~~~

行内代码前后用1个\`扩起来：\`import pandocs as pd\`

\~\~\~ 与 \`\`\` 是等效符号(但有些markdown编辑器不识别)，用于嵌套，即代码块中要显示\`\`\`的情况。

加上语言种类，渲染器会按照这种语言的语法做渲染。

~~~
```python
import pandas as pd
```
~~~

语言定义\`\`\`python和\`\`\`{.python}等效，但后者可以增加更多参数

~~~
```{.python caption="有语言定义的代码块"}
import pandas as pd
```
~~~

代码块原来的目的只是把代码按不同的语法进行渲染，但扩展后就变成强大的活的文字。

# 块引用

```
> 引用文字1
偷懒写法(中间没有空行，所以当作跟上一行同段落，无需再加>号)，“引用文字1”后面要2个空格

> 引用文字2
> 另一种多行块引用写法
```

# 引用书目

引用书目需要单独的.bib文件定义，pandoc会将参考书目渲染在最后

```
[@doe1905]
```

# 导入(md<--docx)

```bash
pandoc --extract-media ./ -t gfm-raw_html src.docx -o tgt.md
```

docx文件可能有wmf/emf文件，可以用libreoffice命令行批量转：

```bash
$ soffice --headless --convert-to png *.emf # 或svg
```

图片外边有大量空白的，可以用ImageMagick的convert命令自适应切除：

```
convert pic1.png -trim pic1.png
```

# 导出(md-->docx)

pandoc可以有很多参数，将自己常用的参数写在~/.pandoc/default/docx.yml中做成缺省配置，就只需：

```
pandoc -d docx myfile.md -o myfile.docx
```

常用临时参数(以ref.docx作为word模板)：

```
pandoc -d docx --reference-doc=ref.docx myfile.md -o myfile.docx
```

