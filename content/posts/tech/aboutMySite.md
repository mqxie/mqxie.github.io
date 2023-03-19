---
title: "HUGO+Github建站总结" 
date: 2023-03-19T12:38:11+08:00 # 创建时间
lastmod: 2023-03-19T12:38:11+08:00 # 更新时间
author: ["mqxie"]
keywords:  # 未设置keyword
- 
categories: # 没有分类界面可以不填写
- 
tags: # 标签
- 
description: ""
weight:  #  输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: fasle # 本页面是否显示评论
reward: false # 打赏
mermaid: true #是否开启mermaid
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示路径
cover:
    image: "" #图片路径例如：posts/tech/123/123.png
    zoom: # 图片大小，例如填写 50% 表示原图像的一半大小
    caption: "" #图片底部描述
    alt: ""
    relative: false
---

# 1.动机

早在读本科时，就已经购买了域名，而且买了10年，那时候用hexo+GitHub做了第一个网站。折腾了两周多，最终建成的网站也挺好，现在回想起来仍有满满的成就感。只可惜，在搞定建站没几天，事情就多了起来，加上换了电脑，原来的本地环境全没了，那个网站就搁浅了。

工作半年多以来，发现能清晰的把一件事情的要害关系分析清楚并讲出来是一种非常罕见的能力，清晰、条理的表达往往使人信服；另外，接触数据中心基础设施建设也有一段时间了，自己也有一些积累和心得，这些事从实践中积累出来的宝贵经验，希望能好好总结下来，恰恰缺少一个相对自由的平台来写这些没人看的玩意。于是，再次萌生了建一个个人网站的想法。

借鉴上次的经验，我重新想了下我要的到底是什么。不是花里胡哨的网站动效，也不是美观漂亮的主题，而是一个能让我方便、快捷地写东西，还要环境简单，易维护，一切从实用出发。有了这个思路，我对比了目前主流的静态网站框架，最终选择了[HUGO](https://gohugo.io/)。Hugo是由Go语言实现的静态网站生成器，简单、易用、高效、易扩展、快速部署。从实践来看，也确实如其官网描述的那样：**The world’s fastest framework for building websites.**

# 2.建站过程

## 2.1巨人的肩膀

最开始我还是想自己折腾HUGO，并且也这么做了。看了几天文档之后，不光效率低，而且与我原本的思路相悖，我要的是一个成熟的博客写东西，而不是再次从头学习静态网站的搭建。走了几天弯路之后，我放弃造轮子，能用现成的就用现成的。

这里要尤其感谢 [**Kevin Xu**](https://github.com/xyming108/) 的贡献，本网站的搭建过程中，大量使用了他的源码，在他的贡献的基础上做了小部分的修改和增减，本网站就成型了，这里放上 **Kevin Xu** 的网站链接[Sulv's Blog](https://www.sulvblog.cn/)，感兴趣的可以去学习。

赠人玫瑰，手留余香，再次感谢。

## 2.2便捷化设置

为了更方便地更新文章，我使用了HUGO网站推荐的Github Action，当源代码push后，将自动渲染部署，比起hexo可方便太多了。关于使用Github Action，网上有很多教程，我这里使用了HUGO官网的[Host on GitHub | Hugo (gohugo.io)](https://gohugo.io/hosting-and-deployment/hosting-on-github/)的推荐方法。需要注意的是，如果按照这种方法，需要将仓库分支名字改为main，默认为master，git修改仓库分支命令为：

```bash
git branch -m [old-name] [new-name]
```

到这一步，写完文章后仍然需要使用Git命令push文章，我这里使用[Github Desktop](https://desktop.github.com/)，写完文章后在GUI界面完成push，然后Github Action自动部署，这应该是目前最顺手、最简单的方案了，部署全程不需要一行代码。

## 2.3写文章

在本地仓库根目录下，使用命令行创建一个新文章:

```bash
hugo new posts/[categoriesName]/[fileName].md
```

其中`categoriesName`有`learn`、`tech`、`read`、`life`，分别对应网站首页的学习、技术、阅读、生活四个分类。

创建文章之后，在对应的文件夹下就会生成相应的`.md`文件，并且已经使用了默认的文章模板，我这里使用[Typora](https://typora.io/)在本地写编写文章，极其方便。文章主体内容完成后，回到Github Desktop，先`commit`然后`Fetch origin`，在网络良好的前提下，两三分钟后就能看到最新更新的文章了。

## 2.4附：增加网站运行时间

使用`<span>`元素将`网站运行时间`与其他页脚内容控制在同一行，在`[blogFileFolder]\layouts\partials\footer.html`文件中的不蒜子代码后添加如下代码

```html
    <!-- 添加网站运行时间 -->
    <span>
        网站已安全运行 <SPAN id=span_dt_dt style="color: #0196e3;"></SPAN> 
        <SCRIPT language=javascript>
        function show_date_time(){
        window.setTimeout("show_date_time()", 1000);
        BirthDay=new Date("3/12/2023 00:00:00");//日期自己修改
        today=new Date();
        timeold=(today.getTime()-BirthDay.getTime());
        sectimeold=timeold/1000
        secondsold=Math.floor(sectimeold);
        msPerDay=24*60*60*1000
        e_daysold=timeold/msPerDay
        daysold=Math.floor(e_daysold);
        e_hrsold=(e_daysold-daysold)*24;
        hrsold=Math.floor(e_hrsold);
        e_minsold=(e_hrsold-hrsold)*60;
        minsold=Math.floor((e_hrsold-hrsold)*60);
        seconds=Math.floor((e_minsold-minsold)*60);
        span_dt_dt.innerHTML=""+daysold+"天"+hrsold+"小时"+minsold+"分"+seconds+"秒";
        }
        show_date_time();
        </SCRIPT>
    </span>
```

种一棵树最好的时间是十年前，其次是现在。出自非洲女作者Dambisa Moyo的著作《dead aid》，书中结束语：The best time to plant a tree was 10 years ago. The second best time is now.

于是我将网站开始时间设置为2023年3月12日植树节。



# 3.未来思路

**严肃写作是有条理地思考。**

希望可以养成一个经常写作总结的习惯，扩大知识面的同时不断完善自己的知识体系，先认识世界才有世界观。



