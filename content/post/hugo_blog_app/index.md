+++
title = 'HUGO博客使用教程'
date = 2026-03-03T00:41:24+08:00
categories = ["速查","博客搭建"]
+++

调试命令：hugo server -D

创建文章：hugo new content post/要创建的文章目录/index.md

删除文章：在 Hugo 中，**没有专门的命令**（比如 `hugo delete`）用来删除文章。

​		要删除一篇文章，你只需要**在你的文件系统中把对应的文件或文件夹直接删掉**就可以了。

GitHub自动上传  （cmd中）

```bash
git init
git add .
git commit -m "%date% %time%"
git branch -M main
git remote add origin {你的github仓库地址}
git push -u origin main
```



git remote add origin {你的github仓库地址}只要使用过一回就不用再配置了



关于自动生成的两个+++号间的内容，如何配置，如下：

# 📝 Hugo + Stack 主题文章配置完全笔记

## 一、 核心概念：Front Matter

在使用 `hugo new` 命令创建文章时，文件顶部被 `+++` (TOML格式) 或 `---` (YAML格式) 包裹的区域称为 **Front Matter**。它不属于正文，专门用于告诉 Hugo 和主题如何解析、渲染和配置这篇文章。

## 二、 文章的基本操作 (创建与删除)

- **创建文章：** `hugo new content post/你的文件夹名/index.md` (这会创建一个 Page Bundle，方便把文章配图和 markdown 放在同级目录)。
- **删除文章：** Hugo 没有删除命令。直接在文件管理器中**删除对应的文件夹** (例如 `content/post/你的文件夹名`) 即可彻底删除。
- **草稿预览：** 本地测试时，需使用 `hugo server -D` 或 `hugo server --buildDrafts` 才能在浏览器中看到 `draft = true` 的文章。

## 三、 Front Matter 属性大全 (TOML 格式)

### 1. 基础与排版 (必填/常用)

```
title = '基于QT的脊柱侧弯监测系统开发'  # 文章显示的标题
date = 2026-03-03T00:25:55+08:00       # 创建或发布时间 (决定时间轴排序)
lastmod = 2026-03-05T10:00:00+08:00    # 最后修改时间
draft = true                           # 草稿状态 (true为隐藏，false为发布)
weight = 1                             # 权重，数字越小在列表越靠前 (常用于置顶)
```

### 2. 内容组织 (Taxonomies)

```
categories = ["嵌入式开发", "项目复盘"] # 文章分类，建议体系化
tags = ["STM32", "C语言", "机械臂"]    # 文章标签，可设置多个，便于检索关联
```

### 3. 展示与 SEO (Stack 主题视觉核心)

```
description = "记录了在准备研究生复试期间，梳理数据结构核心考点的过程。" # 文章摘要，显示在标题下方及供搜索引擎读取
summary = "同上，Hugo原生摘要字段，通常与 description 二选一"
image = "cover.jpg" # 封面特色图。直接将图片保存在 index.md 同级目录并填入文件名即可
```

### 4. Stack 主题专属高级开关

```
math = true                 # 开启数学公式渲染 (KaTeX/MathJax)，包含复杂推导时设为 true
comments = false            # 单独关闭本文的评论区
license = "CC BY-NC-ND 4.0" # 在文章底部声明特定的版权协议
hidden = true               # 隐藏文章 (不在首页和归档列表中显示，但知道链接可直接访问)
color = "#ff5733"           # 自定义文章在主页卡片上的主题色 (不填则自动从封面图提取)
```

### 5. 外部链接卡片

在文章末尾自动渲染出漂亮的外部链接卡片，适合指向代码仓库或参考资料：

```
[[links]]
  title = "GitHub 源码"
  description = "包含 PyTorch 模型训练代码与数据集整理脚本"
  website = "https://github.com/..."
  image = "https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png"
```

## 四、 进阶技巧：自定义默认模板 (Archetypes)

如果不想每次新建文章都手动敲这些属性，可以修改博客根目录下的 **`archetypes/default.md`** 文件。将其内容替换为你最常用的组合，例如：

```
+++
title = '{{ replace .Name "-" " " | title }}'
date = {{ .Date }}
draft = true
description = ''
image = ''
categories = ['']
tags = ['']
math = false
+++
```
