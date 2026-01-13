---
title: UABS 维基 - 使用手册
published: 2025-07-23
description: 'UABS 的 使用手册'
image: ''
tags: [Game, Unity, UABS]
category: Tutorial
draft: false
lang: zh      # Set only if the post's language differs from the site's language in `config.ts`
---

::github{repo="PapayaModding/UABS"}

<p align="center">
    <img src="/marblestack/imgs/az/a/logo.png" width="300"/>
</p>

教程使用版本 [v1.0.3-Beta](https://github.com/Kolyn090/UABS/releases/tag/v1.0.3-beta)。

⛳ 特注：我已经将可管理缓存(manual cache)重新命名为资源容器(package)。如果你使用的是v1.0.3-Beta以外的版本请务必注意。

# 📘 使用手册

欢迎阅读**UABS使用手册**。该手册会教你如何使用UABS - 从打开软件到完成复杂的任务。

❗制作模组是一项复杂的工程，这也是为什么UABS不通过阅读手册会难以使用。请仔细阅读手册！

---

## 🧭 目录

1. [启动软件](#getting-started)
2. [交互界面概要](#user-interface-overview)
3. [打开资源包文件](#opening-a-bundle-file)
4. [制作可管理缓存](#building-manual-cache)
5. [搜索资源包](#searching-for-bundles)
6. [查看和提取资源文件](#viewing-and-exporting)
7. [资源笔记系统](#asset-memo)
8. [依赖项跳转](#dependency-navigation)
9. [解决问题](#troubleshooting)

<br>

<a name="getting-started"></a>
## 🟢 启动软件

1. 在[这里](https://github.com/Kolyn090/UABS/releases)下载任意版本。
2. 解压后打开里面叫‘UABS'的可执行文件，或者使用Unity版本如果你使用的是开发环境。

<img width="700" alt="getting-started1" src="https://github.com/user-attachments/assets/7f216209-d70f-4537-905f-6f942ab395de" />

> 💡 **特注：UABS的开发环境和实验环境都集中在Unity 2021.3.33f1这个版本。

<br>

<a name="user-interface-overview"></a>
## 🖥️ 交互界面概要

| 选项 | 说明 |
| --- | --- |
| 文件 | - 📄打开文件：在 UABS 中打开文件（仅支持 ".bundle"、".ab"、".assets" 文件）<br>- 📁打开文件夹：打开文件夹并搜索上述类型的文件。 |
| 提取 | - 🌌提取全部：提取包中的所有资源（目前仅支持图片）<br>- 👆提取选中项：提取包中所有选中的资源（目前仅支持图片）<br>- 🧱提取过滤结果：提取包中所有被过滤的资源（目前仅支持图片）<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ 仅适用于查看资源包时。 |
| 搜索 | - 🔑按关键词：查找名称中包含任意关键词的所有资源包，或其中任意资源名称包含关键词。关键词用英文或中文逗号分隔，例如：hero,weapon,skill。如果结果中包含排除关键词，则不会被加入结果。<br>- 🖼️按图片：使用 Sprite / Texture2D 搜索资源包（仅按名称比对，不比对像素）。<br>- 📝按笔记：与“按关键词”类似，但搜索对象为笔记内容。<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ 使用此功能前需要先构建可管理缓存。 |
| 依赖 | - 🧩搜索资源包依赖项：将依赖的资源包显示为文件夹视图。<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ 使用此功能前需要先构建可管理缓存。<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ 仅适用于查看资源包时。 |
| 筛选 | - 🧱根据资源类型（AssetClassID）筛选资源包中的资源。<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ 仅适用于查看资源包时。 |
| 笔记 | - 📂选择笔记缓存：指定一个可管理缓存用于笔记存储。<br>- 🧬继承笔记：将旧游戏版本中的笔记迁移到新版本。支持三种模式：<br>&nbsp;&nbsp;&nbsp;&nbsp;* 安全：如果当前版本该项笔记非空，则不迁移。<br>&nbsp;&nbsp;&nbsp;&nbsp;* 覆盖：若旧版本该项笔记非空，则覆盖当前笔记。<br>&nbsp;&nbsp;&nbsp;&nbsp;* 强制：只要匹配就进行迁移。<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ 使用此功能前需要先构建可管理缓存。 |
| 缓存（可管理缓存） | - 🗃️构建新缓存：点击“Build New Cache”按钮开始构建。选择游戏数据文件夹（如 StreamingAssets(PC)、split_UnityDataAssetPack(Android)）。接着，你需要在 UABS_Cache 文件夹下创建一个新文件夹并选择它。等待进度完成（滚动视图中的条目会从灰变白）。<br>- 🗑️删除缓存：点击“X”按钮可删除已有缓存。 |
| 返回 | - ↩️返回：点击此按钮返回。如果当前在查看资源包中，将返回其所在文件夹；如果在文件夹中，将返回上层文件夹；如果在依赖或搜索视图中，将返回上一个视图。 |

<br>

<a name="opening-a-bundle-file"></a>
## 📂 打开资源包文件
在工具栏，将鼠标悬停在 File 选项 然后选择 Open File。

<img width="700" alt="opening-a-bundle1" src="https://github.com/user-attachments/assets/e2a67849-bfc9-431a-a757-d8ecbe7258a4" />

打开一个带有 bundle 后缀的文件。

<img width="788" height="280" alt="opening-a-bundle2" src="https://github.com/user-attachments/assets/8a80d327-3c37-46f6-93ce-307ca4c6b368" />

大功告成！

<img width="700" alt="opening-a-bundle3" src="https://github.com/user-attachments/assets/a09e554e-a445-405e-9345-fa30d3084e64" />

> ⚠️ **特注：** 由于当前的读写性能限制，加载大型文件可能需要一些时间。

<br>

<a name="building-manual-cache"></a>
## 🗃️ 制作可管理缓存

选择 Cache -> Build New Cache -> Build New Cache。

<img width="700" alt="building-manual-cache1" src="https://github.com/user-attachments/assets/ebfbe508-5a24-45fc-b5ea-c45064e4b3c4" />

选有游戏数据的文件夹。

> 如果你的游戏是在Windows上并且是在Steam下载，一般来说它的位置为 '~/steamapps/common/[GAME]/[GAME]_Data/StreamingAssts/aa/StandaloneWindows64'。

> 如果是安卓APK文件的话，一般来说在 '~/split_UnityDataAssetPack/assets/aa/Android'。

<img width="229"  alt="building-manual-cache2" src="https://github.com/user-attachments/assets/09bfc403-bd2f-46cd-8cb1-1433c2e5e6cc" />

在选择了游戏数据文件夹后，在 UABS_Cache 文件夹里创建一个新的文件夹（需要你创建）然后并选中它。我推荐你建该文件夹以该方式取名：【游戏】-【版本】。比如，如果你的游戏叫 OWL 而且版本是 2.11.0.2，就这样做：

<img width="742" alt="building-manual-cache3" src="https://github.com/user-attachments/assets/67f7d0cf-ab87-4cd7-a208-1da72e968add" />

再次打开 Build New Cache 界面，你将看到一个背景为灰色的新条目。是灰色的话就说明 UABS 还在处理游戏数据文件夹。

<img width="231" height="185" alt="building-manual-cache4" src="https://github.com/user-attachments/assets/cc223746-f1a2-445a-bd7d-41cdf112cfbb" />

在 UABS 完成后，它的背景颜色会变成白色，如图所示：

<img width="232" height="185" alt="building-manual-cache5" src="https://github.com/user-attachments/assets/832475cb-b8f9-42af-bb5c-6f8a8f160f3f" />

🎉 好的，你现在在 UABS 有了一个属于你的可管理缓存了！你将会在很多地方用得上它。

<br>

<a name="searching-for-bundles"></a>
## 🔍 搜索资源包

你可以在 UABS 中搜索资源包。比如，使用关键词搜索。在 Search -> By Keywords 选择一个可管理缓存。

<img width="700" alt="searching-for-bundles1" src="https://github.com/user-attachments/assets/8ff0bc21-ea00-46d0-be53-c274054cbc6c" />

在你选择了缓存后，该条目会变成白色。

<img width="224" height="93" alt="searching-for-bundles2" src="https://github.com/user-attachments/assets/10bbc65b-5fc5-472e-9146-420bc8aa04fa" />

现在按照指示输入你的关键词（以及排除关键词，如果有的话）。在你完成后，点击 Search。

<img width="225" height="223" alt="searching-for-bundles3" src="https://github.com/user-attachments/assets/21b094fc-ab86-4529-b896-ec532ab6b119" />

如果有任何资源包被找到，它们会被展示出来。

<img width="700" alt="searching-for-bundles4" src="https://github.com/user-attachments/assets/73093a6d-e74c-4bd9-9125-3a70de75f979" />


<br>

<a name="viewing-and-exporting"></a>
## 🖼️ 查看和提取资源文件

**目前，UABS 仅支持对 Sprite 和 Texture2D 文件的查看和提取。**

要查看文件的话只需要点击资源的条目。如果它是被 UABS 支持的文件格式的话显示屏会进行展示。如果是图片样式的文件你还可以放大缩小和移动来辅助你查看。

<img width="700" alt="viewing-and-exporting1" src="https://github.com/user-attachments/assets/9906ca37-45ff-4254-afac-a2855728dc3b" />

要提取资源的话，选择 Export -> Export all assets。然后选中一个地方来保存。

<img width="700" alt="viewing-and-exporting2" src="https://github.com/user-attachments/assets/99a230cb-e7d2-47a0-881b-e9b24ee29ab8" />

在你打开了提取的文件夹后，你应该会看到类似以下的内容：

<img width="322" height="143" alt="viewing-and-exporting3" src="https://github.com/user-attachments/assets/bfa9fc0d-d849-47bc-9d9c-a486e392f059" />

<br>

<a name="asset-memo"></a>
## 🏷️ 资源笔记系统

你可以使用笔记功能来实现快速导航、添加注释或进行项目整理。但是首先必要的是，你需要开启它。到 Memo -> Select Memo Cache，选择一个可管理缓存。还是一样，条目被点击后会变成白色，说明正在使用中。

<img width="700" alt="asset-memo1" src="https://github.com/user-attachments/assets/2f4cfd42-c8d1-4e80-9d69-43346f51404e" />

执行上述操作后，笔记会变为可用。（请注意，目前仅支持 Sprite 和 Texture2D 类型的资源，对于其他类型的资源，该字段仍将处于禁用状态。）

<img width="321" height="187" alt="asset-memo2" src="https://github.com/user-attachments/assets/b5f92292-74a1-47dd-9a84-6b36cd3263e6" />

你可以在笔记中输入文字，比如：

<img width="321" height="194" alt="asset-memo3" src="https://github.com/user-attachments/assets/af74bba2-6bec-4997-a44e-05c7fdb8aade" />

🎉 恭喜你在 UABS 完成了第一个笔记！

现在来试试看用笔记搜索吧。到 Search -> By Memo，输入关键词来查找资源包。你不需要一字一顿地查找。例如你的笔记是 哈利波特：消失的密室，那么你搜索 哈利波特 也能找到。

<br>

<a name="dependency-navigation"></a>
## 🔗 依赖项跳转

UABS 对待依赖项的方式和其他工具有所不同。你可以移动到依赖项的依赖项里，这样一直查找下去都没问题。该操作在 UABS 非常简单，你只需要去 Depend -> 选择一个可管理缓存的条目。

它会自动搜索所有依赖项资源包。就比如这个例子：

<img width="700" alt="dependency-navigation2" src="https://github.com/user-attachments/assets/5e32538c-09fd-43b9-a81d-67559d57de62" />


<br>

<a name="troubleshooting"></a>
## 🧯 解决问题

UABS 的测试力度很低，而且所有 UI 都是我重头开始写的。遇到问题是很正常的。不过如果你真的遇到了问题，请到 C:\Users\【你的用户名】\AppData\LocalLow\DefaultCompany\UABS 找到 Player.txt。发一个 issue 然后把这个文件发给我。也请记得告诉我怎么复原你遇到的情况，这样我可以更好地修复。

<br>

## 🙏 万分感谢你使用 UABS ！

如果你喜欢这个项目的话，可以考虑给我的 repo 一颗⭐！

欢迎自由浏览其他维基页面以获取更多详细信息。

