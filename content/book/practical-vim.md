---
title: "Practical Vim"
date: 2014-11-13 22:11
---

[TOC]

## 第一章 .(dot)命令 ##

> `.` 命令可以重复上次的修改

Vim把进入插入模式到退出形成一次修改, `i{insert something}<Esc>`(@todo, 在插入模式中移动光标会重置修改状态)

`>G` 增加从当前行到文档末尾的缩进层级

`A` 在当前行的结尾添加内容(等价`$a`), 类似还有:

* `C` = `c$`
* `s` = `cl`
* `S` = `^c`
* `I` = `^i` 

查找:

* `f{char}` 行内查找下一处指定字符出现的位置, 使用`;` 重复上次查找, 使用`,`回退
* `F{char}` 行内查找上一个指定字符
* `/{pattern}` 和 `?{pattern}` 分别是文档中查找下/上一处匹配, 重复是`n`, 回退是`N`

## 第二章 普通模式(Normal Mode) ##

> 如果在插入模式使用了上下左右光标键，会产生一个新的撤销块 (P16)

> 构造一个可重复的撤销块 (配合 点`.`操作符使用)

<http://vimgolf.com/> 尽量用最少的按键次数实现一个操作, 一个有趣的网站

简单的算数运算:

> `<C-a>` 和 `<C-x>` 会把当前光标之上或之后的数值加1/减1
> `count<C-a>` 会把数值加上 [count]

这个依然可以配合点操作符

`cW` 从当前光标删除一个单词.

> 能够重复，就别用次数

@todo 12 chapter

## 第三章 插入模式(Insert Mode) ##

在插入模式中更正错误，如果出错的位置在单词开头，删除整个单词再重新输入比退格键要快.

`<C-h>` 删除前一个字符(类似退格键)
`<C-w>` 删除前一个单词
`<C-u>` 删至行首

`<C-[>` 和`<Esc>` 类似，也是切换到普通模式
`<C-o>` 切换到 `插入-普通模式`, 是普通模式的一个特例, 进入此模式，执行一个普通模式命令后，会自动切换回插入模式.

`zz` 命令可以重绘窗口，使当前行在窗口居中.

使用`<C-o>`配合`zz`(即`<C-o>zz`)可以方便的在插入模式写代码时，让当前行从末尾移到屏幕中央.

`K` 查看光标下单词的手册页
`J` 把当前行和下一行连接在一起

@todo 寄存器 tip 15, P 28

在插入模式中, 使用`<C-r>=`可以使用寄存器做运算.

	<i><C-r>=(40+60)*5 + 500/10<CR>

`C-v{code}`, 其中{code}是要插入的字符编码

	# 输入A
	<C-v>065

	# 输入一个unicode,
	# :h i_CTRL-V _digit
	<C-v>u00bf

光标移到字符上，使用`ga`可以查看它的编码.

`<C-k>{char1}{char2}` 二合字母(digraph)可以打出一些特殊字符

	# 字符 «
	<C-k><<

@todo tip 19 P33, 虚拟替换模式

## 第四章 可视模式(Virtual Mode) ##

可视模式有三种:

* 字符文本
* 行文本
* 块文本
