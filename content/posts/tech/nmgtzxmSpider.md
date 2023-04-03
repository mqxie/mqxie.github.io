---
title: "python爬取内蒙古投资项目在线审批办事大厅项目列表" 
date: 2023-04-04T01:30:30+08:00 # 创建时间
lastmod: 2023-04-04T01:30:30+08:00 # 更新时间
author: ["mqxie"]
keywords:  # 未设置keyword
- 
categories: # 没有分类界面可以不填写
- 
tags: # 标签
- 爬虫
- python
- spider
description: ""
weight:  #  输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: true # 是否为草稿
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
# 环境准备

conda、python环境、requests库、beautifulsoup库、pycharm

# HTML基础

<a>标签为链接，href值为目标要跳转的URL地址。

    表格
    <table>是用来定义表格的标签，里面一般会嵌套和表格相关的元素。
    <thead>表示表格的头部，一般是表格的第一行
    <tbody>表示表格的主体
    <tr> table row表格行
    <td> table data 每一个单元格表示一项项数据

# 提取思路

1. 首先提取1个项目，将项目编号、项目名称、建设内容等信息写到excel中。
2. 提取一页中10个项目，写到excel中。
3. 批量读取两页总计20个项目，写道excel中。
4. 批量读取多页。
5. 设置时间为截止条件，实现特定日期前项目信息的批量写入。



```python
import requests
from bs4 import BeautifulSoup

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36"
}

response = requests.get("http://nmg.tzxm.gov.cn/tzsp/VDEdfsef.jspx", headers=headers)
print(response.status_code)

# # 测试
# if response.ok:
#     print(response.text)
# else:
#     print("请求失败")

content = response.text
soup = BeautifulSoup(content, "html.parser")

# 项目编码
firsttable = soup.find("table")
print(firsttable)

```




