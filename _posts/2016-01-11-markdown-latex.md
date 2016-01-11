---
layout: post
title: "关于markdown语法及latex公式的编辑"
description: "摸索了一段时间，很遗憾，markdown确实不支持latex公式的编辑和编译，采用markdownpad进行公式的编辑一直就是一个揪心的问题，这里首先简单介绍了markdown常用的语法，然后采用sublime+mathjax提供了一种替代的公式插入方法，仅供参考."
category: 'project experience'
---

Markdown常用语法总结
---
# 1. 标题

Markdown语法：

    # 一级标题
    ## 二级标题
    ### 三级标题
    #### 四级标题
    ##### 五级标题
    ###### 六级标题
效果

#一级标题
##二级标题
###三级标题
####四级标题
#####五级标题
###### 六级标题
#2. 粗体、斜体
Markdown语法：

    **粗体**
    __粗体__
    *斜体*
    _斜体_
效果

**粗体**
__粗体__
*斜体*
_斜体_

#3. 分割线
Markdown语法：

    ---
    ***

效果

---
***

#4. 列表
Markdown语法：

    - 无序列表项目
    
    * 无序列表项目
    
    1. 有序列表项目
    2. 有序列表项目
    
    - 外层列表项目
     + 内层列表项目
     + 内层列表项目
    - 外层列表项目

效果

- 无序列表项目

* 无序列表项目

1. 有序列表项目
2. 有序列表项目

- 外层列表项目
 + 内层列表项目
 + 内层列表项目
- 外层列表项目

#5. 添加超链接、图片
Markdown语法：

    [简书](http://chuantu.biz/t2/24/1452517678x-1376436574.jpg)
    ![简书slogan](http://chuantu.biz/t2/24/1452517678x-1376436574.jpg)

    [简书][1]
    ![简书slogan][2]
    
    [1]:http://chuantu.biz/t2/24/1452517678x-1376436574.jpg
    [2]:http://chuantu.biz/t2/24/1452517678x-1376436574.jpg

效果

[简书](http://chuantu.biz/t2/24/1452517678x-1376436574.jpg)
![简书slogan](http://chuantu.biz/t2/24/1452517678x-1376436574.jpg)

[简书][1]
![简书slogan][2]

[1]:http://chuantu.biz/t2/24/1452517678x-1376436574.jpg
[2]:http://chuantu.biz/t2/24/1452517678x-1376436574.jpg

# 6. 添加表格
Markdown语法：

| ABCD | EFGH | IJKL |
| -----|:----:| ----:|
| a    | b    | c    |
| d    | e    |  f   |
| g    | h    |   i  |


ABCD | EFGH | IGKL
-----|------|----
a    | b    | c
d    | e    | f
g    | h    | i

#7. 添加代码
Markdown语法：

`Tab`或四个空格（大段文字添加代码框，每行前添加）

	123456789

#8.引用
Markdown语法：

> 引用的文字

> 引用的文字

> 引用的文字

------
  
> 引用的文字
>> 引用的文字 


#9. 单行长文字
Markdown语法：

在需要以单行长文字显示的文字段落前加四个空格

    单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字单行长文字

#10. 首行缩进
Markdown语法：

 缩进一个字符缩进一个字符缩进一个字符缩进一个字符缩进一个字符缩进一个字符

 缩进两个字符缩进两个字符缩进两个字符缩进两个字符缩进两个字符缩进两个字符

  缩进四个字符缩进四个字符缩进四个字符缩进四个字符缩进四个字符缩进四个字符

#11. 添加脚注
Markdown语法：

A[1]
[^1]:aaaa

    A[1]
    [^1]:aaaa

#12. 创建链接
为输入的URL或邮箱自动创建链接，如test@domain.com。

Markdown语法：

    <test@domain.com>
预览效果：
<test@domain.com>

#13. 转义字符
在特殊字符，如*、[、>等前面加\可使特殊格式字符转换为正常字符打出（有序列表符号如1.，须在. 前加\）。

Markdown语法：

    \\
    \`
    \*
    \_
    \{\}
    \[\]
    \(\)
    \#
    \+
    \-
    \.
    \!

\\
\`
\*
\_
\{\}
\[\]
\(\)
\#
\+
\-
\.
\!


Markdown公式插入
---

采用Sublime Text 2 + OmniMarkupPreviewer的方法进行替代不能使用latex的小bug

#1.Sublime Text 2 + OmniMarkupPreviewer安装方法
首先，再行下载Sublime Text，可以选择简体中文版

安装：

    1.在Sublime Text中安装Package Control
    2.在Sublime Text中打开命令面板（Ctrl+Shift+P）
    3.输入“Install”，然后选择“Package Control: Install Package”
    4.选择“OmniMarkupPreviewer”
这样子就自动安装了这个插件。

OmniMarkupPreviewer中支持LaTeX的使用说明：
1.设置。公式的渲染使用了MathJax库，所以需要在OmniMarkupPreviewer的设置中，将"mathjax_enabled"设置为“true”。之后MathJax会在后端自动下载。
![](http://chuantu.biz/t2/24/1452519806x-1376436574.bmp)

#2.下载MathJax并配置：

    https://github.com/downloads/timonwong/OmniMarkupPreviewer/mathjax.zip
然后解压到下面的目录里：

    Sublime Text 2\Packages\OmniMarkupPreviewer\public
覆盖文件夹里面methjax文件夹

之后在目录“Sublime Text 2\Packages\OmniMarkupPreviewer”中创建一个空文件MATHJAX.DOWNLOADED
这样子MathJax就安装成功了。

测试，输入下面内容：

    ##测试##
    
    This expression $\sqrt{3x-1}+(1+x)^2$ is an example of a $\LaTeX$ inline equation.
    he Lorenz Equations:

$$
\begin{aligned}
\dot{x} & = \sigma(y-x) \\
\dot{y} & = \rho x - y - xz \\
\dot{z} & = -\beta z + xy
\end{aligned}
$$


在Sublime Text 2中使用命令：
![](http://i.niupic.com/images/2016/01/11/l2Bdfh.bmp)

Ctrl+Alt+O：在浏览器中预览

Ctrl+Alt+X：输出为HTML文件

Ctrl+Alt+C：复制为HTML文件

效果如下：
![](http://chuantu.biz/t2/24/1452519913x-1376436574.bmp)

###**（mathjax语法与latex稍有不同，直接采用CEdit工具生成公式然后保存图片也是可以的，至于哪个更好用那就是仁者见仁智者见智了）**

免费图片上传网站：
http://chuantu.biz/

https://www.niupic.com/index.html

**感谢简书作者的分享**

参考：[Markdown入门学习小结](http://www.jianshu.com/p/21d355525bdf)

参考：[使用Markdown的时候需要插入LaTeX公式方法](http://blog.163.com/hailin_xin/blog/static/2181621902013112410215608)



