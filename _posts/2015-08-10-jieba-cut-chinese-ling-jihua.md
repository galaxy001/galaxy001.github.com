---
layout: post
date: 'Mon 2015-08-10 18:47:28 +0800'
slug: "jieba-cut-chinese-ling-jihua"
title: "\“结巴\”中文分词 与 \“令完成已经完成令计划的计划\”"
description: ""
category: 
tags: Programming, Joke
---
{% include JB/setup %}

源起是这则推文：

`把“令完成已经完成令计划的计划”这个新闻标题分词之后发到群里的结果`

![令完成已经完成令计划的计划](/assets/images/2015/jieba.cut.png)

<blockquote class="twitter-tweet" lang="en"><p lang="zh" dir="ltr">把“令完成已经完成令计划的计划”这个新闻标题分词之后发到群里的结果，哈哈。标题出处的微博在这里<a href="http://t.co/qtS2vnVmRN">http://t.co/qtS2vnVmRN</a> <a href="http://t.co/dzmEIOBb0Q">pic.twitter.com/dzmEIOBb0Q</a></p>&mdash; RMS门下走狗 (@ggarlic) <a href="https://twitter.com/ggarlic/status/630678454652919808">August 10, 2015</a></blockquote>

微博链接当然被和谐了，但咱对`jieba`的出现有些好奇，就g了下，然后
发现 结巴分词 有一堆语言版本……

最初的应该是Python版本，fxsjy/jieba 的 [结巴中文分词](https://github.com/fxsjy/jieba)。
同时搜到的还有 PHP版，fukuball/jieba-php 的 [目前翻譯版本為 jieba-0.19 版本](https://github.com/fukuball/jieba-php)。
然后就是 R语言版，qinwf/jiebaR 的 [jiebaR 中文分词](https://github.com/qinwf/jiebaR/)。

最后，网上说有C/C++的，于是咱再搜，终于找到了，是[Yanyi Wu](https://github.com/yanyiwu)写的。
包括[yanyiwu/cppjieba](https://github.com/yanyiwu/cppjieba), [yanyiwu/cjieba](https://github.com/yanyiwu/cjieba)。
以及[清爽头文件库的 yanyiwu/libcppjieba](https://github.com/yanyiwu/libcppjieba), [yanyiwu/nodejieba](https://github.com/yanyiwu/nodejieba)。

然后，有个["结巴"中文分词系列性能评测](http://yanyiwu.com/work/2015/06/14/jieba-series-performance-test.html)。

额，就酱啦。
懒得开个repo去整理加mirror。理论上这种没有政治问题的软件不会被自主规制才对。而且fork的人也不少，咱就不fork了。  
其实是咱现在用不上，的说。
