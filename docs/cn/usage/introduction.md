# 程序介绍

---

## 概述

随着人工智能的快速发展，大模型API已经廉价到几乎不要钱的程度。要知道，人工智能的自然语言处理技术，天然具备翻译属性，在这种高性价比基础资源肥沃的环境下，除了法务、财务类要求特别严谨的文档翻译场景，请问你还愿意花高价钱去找翻译公司翻译文件吗？尤其是一些通用场景下，仅对外文文件做初步翻译阅读即可，要求并不高，例如外贸询盘附件、外文文献资料、外文书籍与期刊等等，这类文件讲求的是通读全文，快速理解。

除此之外，我们把待翻译的材料打包交给了翻译公司或者翻译软件，即使签订了数据保密协议，数据安全性也不见得得到保护，依旧有产生泄露的风险。

是否有这样的工具能够结合人工智能API（API可以是开源大模型API，也可以是闭源大模型API），为我们做这样翻译文档的事情呢？

有，EZ-work AI文档翻译程序就是基于以上需求诞生，无论你是在校学生、在职人员、创业者还是企业，只要你想低成本、快速、高质量翻译文档，甚至对数据保密性也有要求，EZ-work AI都能祝你一臂之力！

EZ-work AI文档翻译拥有以下主要功能特色：

- 多种部署方式任选
- 社区版完全开源免费
- 支持批处理和多线程
- 支持兼容OpenAI格式任意API
- 支持翻译txt/word/md/csv/excel/pdf/ppt/扫描件

目前，EZ-work AI文档翻译已上线开源版本，项目处于建设初期。

项目地址:

>Github：https://github.com/EHEWON/ezwork-ai-doc-translation

> 演示地址：https://ezdemo.erui.com/

## 使用方式

### 1. 在线使用

如果你对应程序开发与部署不太了解，我们推荐直接通过EZ-work AI官方部署的**演示版**程序在线使用，本程序采用高性能、大带宽物理机搭建，拥有超高稳定性且能够支持多人高并发调用。访问地址：

[https://ezdemo.erui.com](https://ezdemo.erui.com)

[如何使用？](/cn/usage/community.md)

>- 优点：
>   - 即开即用，快捷方便
>   - 无需依赖本地服务器
>   - 性能优越
>   - 版本同步更新
>- 缺点：
>   - 数据库非私有化
>   - 线程数有一定的限制
>   - 无法云端存储

### 2. 私有化部署

私有化部署需要你具备一定的计算机基础，可以通过我们的[Github仓库>>](https://github.com/EHEWON/ezwork-ai-doc-translation)实现部署。

[如何部署？](/cn/deploy/introduction.md)

>- 优点：
>   - 数据库私有更安全
>   - 并发无限制
>   - 支持二开
>   - 支持云端存储
>- 缺点：
>   - 需要自行部署与更新版本
>   - 依赖本地电脑或服务器性能

## 技术选型

| **类别**      | **技术**            | **注释**                                                   |
| :------------ | :------------------ | :-------------------------------------------------------- |
| 前端框架      | Vue.js 3            | 现代JavaScript框架，适合构建用户界面和单页应用。       |
| 后端框架      | PHP 8.2             | 支持最新特性的PHP版本，适合构建动态网页和API。       |
| 数据库        | MySQL 5.7+          | 关系数据库管理系统，稳定且高性能，广泛应用于Web应用。   |
| Web 服务器    | Nginx               | 高性能反向代理和负载均衡器，适合服务静态内容和API请求。 |
| 图像识别      | OpenAI               | 用于高效的图像识别和处理服务。                              |
|                | PyTesseract         | Python包装的Tesseract OCR，支持文本识别。               |
| PDF翻译      | pdf2docx            | 将PDF文件转换为docx格式的工具。                       |
|                | docx2pdf            | 将docx文件转换为pdf格式的工具。                       |
| 其它工具      | python-docx         | 用于创建和修改Microsoft Word文档的Python库。          |
|                | python-pptx         | 用于创建和修改Microsoft PowerPoint演示文稿的库。      |
| Node.js       | Node.js 22+         | JavaScript运行环境，适合构建高并发的后端服务。          |
| Python        | Python 3+           | 高级编程语言，功能强大，适合处理各种数据处理任务。        |

### 说明

- 以上技术选型是根据项目需求而定，确保在视觉效果、性能和扩展性上达到最佳效果。
- 每种技术都有其特定的优势，根据具体需求选择最优方案，同时保持技术栈的简洁一致性。

## 贡献指南

欢迎贡献、建议、错误报告和修复！对于新功能、组件或扩展，请先在[Github>>](https://github.com/EHEWON/ezwork-ai-doc-translation/issues)开一个 issue 进行讨论，然后再提交 PR。对于参与贡献者我们计划会在后续的进展中给予不定形式的奖励。包括但不限于：

- 现金奖励
- 物质奖励
- 线下互动
- 功能特权

## 开源许可证

本开源项目遵循MIT许可。

```
MIT License

Copyright (c) 2024 LibreChat

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

## 开发计划

2024年我们计划完善社区版核心功能：

- 便捷的部署方式
- 支持翻译更多种类的文档格式
- 支持高质量的扫描件与图片翻译
- 支持语料库功能
- 在线预览
- 多轮翻译

## 微信社群

欢迎加入我们的微信交流群，如需加入，请添加微信好友邀请进入：sunsky89757