---
title: 战魂铭人 - 进阶模组教程2
published: 2025-06-02
description: 'Steam 版本战魂铭人的>>更加进阶版<<模组制作教程'
image: './imgs/test.png'
tags: [Game, OWL, Unity]
category: Tutorial
draft: false
lang: zh      # Set only if the post's language differs from the site's language in `config.ts`
---

::github{repo="PapayaModding/Otherworld-Legends-Mod"}

在阅读本教程前，请先学习[基础教程](/marblestack/posts/a_unity/a_owl/a1_basic_zh/)和[进阶教程](/marblestack/posts/a_unity/a_owl/b1_advanced_zh/)。

作者：Kolyn090

教程游戏版本：v2.10.0

使用Windows x64

教程日期：6/2/2025

本教程将指引你修改储存在SpriteAltas的图像。

<figure style="text-align:center;">
  <img 
    src="/marblestack/imgs/aa/c/test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="dotpict-interface"
  />
  <figcaption style="font-size:0.85rem; color:#666; margin-top:0.4rem;">
    （成果展示，沙包）
  </figcaption>
</figure>

如果你已经尝试使用在进阶教程中描述的方式修改除人物Sprite以外的大部分图像，
你应该会发现该方法对其几乎不奏效。这是因为它们使用的是SpriteAltas打包方法。
其中很大一部分原因是因为文件的引用无法对号。

当你学会本教程以后，你应该可以修改大部分游戏图像而不受源图像大小限制。

:::important[警告]
模组修改可能带来未知风险，包括游戏不稳定、存档损坏、兼容性问题，甚至安全漏洞。切记备份游戏文件，并谨慎操作。
风险自担——如果出现问题，我无法承担责任。
:::

:::important[警告]
该教程的操作流程非常复杂而且繁琐，请仔细阅读每一步。如果你遇到问题可以发issue提问。
:::

### 步骤1️⃣
本教程将使用客厅中的沙包作为示例。（在我的电脑）它的文件位置为：

```txt
"C:\Program Files (x86)\Steam\steamapps\common\Otherworld Legends\Otherworld Legends_Data\StreamingAssets\aa\StandaloneWindows64\graphiceffecttextureseparatelygroup_assets_assets\sprites\unit\unit_other_pile.psd_0678876b821c494df01ee1384bec84f2.bundle"
```

然后是要替换的图像：

<figure style="text-align:center;">
  <img 
    src="/marblestack/imgs/aa/c/sactx-0-128x128-BC7-unit_other_pile-1aae59fd.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="dotpict-interface"
  />
  <figcaption style="font-size:0.85rem; color:#666; margin-top:0.4rem;">
    Credit: https://www.spriters-resource.com/pc_computer/pizzatower/sheet/193192/
  </figcaption>
</figure>

接着，打开进阶教程中的Unity项目。找到Texture2D。

<img 
    src="/marblestack/imgs/aa/c/texture2d_folder.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_folder"
/>

我这里建议把之前关于天人道boss的教程放在另一个文件夹里。然后创建一个新的文件夹，比如叫
‘Other_Pile’。

把要替换的图像放在Other_Pile里。接着在Inspector修改它的参数。

请确保：
1. Texture Type是Sprite(2D and UI)
2. Sprite Mode是Multiple
3. Mesh Type是Full Rect
4. 关闭Generate Physics Shape
5. 开启Read/Write
6. Filter Mode是Point(no filter)
7. Compression是None
8. 点击Apply

这次我们要手动修改Spritesheet（Slice Sprites）。点击Sprite Editor。

首先是沙包的底座。这里我们没有底座，所以直接找个空白的地方画框就行。
**一定要注意要取和示例里一样的名字。**

<img 
    src="/marblestack/imgs/aa/c/pilebase.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="pilebase"
/>

然后是沙包的第一帧。我们这里在左边的雕像画框。切记把Pivot调成Bottom Center。
你也可以用Custom如果会的话。

<img 
    src="/marblestack/imgs/aa/c/pile0.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="pile0"
/>

接下来还有七帧，全部都画在右边的雕像。切记把Pivot调成Bottom Center。
取名见下方图像。
完成后点击Apply，你应该会看见和图片里一模一样的Sprites。

<img 
    src="/marblestack/imgs/aa/c/pile_names.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="pile_names"
/>

### 步骤2️⃣

在Unity的Project Settings里面，找到Sprite Packer-> Mode并调成
Sprite Atlas V1 - Always Enabled。

<img 
    src="/marblestack/imgs/aa/c/proj-setting.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="proj-setting"
/>

接着，在Texture2D里鼠标右键，找到并创建Sprite Atlas。
将其取名为‘unit_other_pile’

<img 
    src="/marblestack/imgs/aa/c/create_atlas.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="create_atlas"
/>

接着调它的参数。把Filter Mode调成Point。
Compression调成None。
然后把我们刚才切好的Sprites全部放到Packables中。
(⚠️ 似乎只能一个一个放，不过东西不多所以无伤大雅)

然后就是最重要的，和之前一样，要把这个文件打包。
名字取 ‘sactx-0-128x128-bc7-unit-other-pile’。

<img 
    src="/marblestack/imgs/aa/c/atlas_setting.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="atlas_setting"
/>

对了，把之前的Texture2D也放里面。

<img 
    src="/marblestack/imgs/aa/c/texture2d_pack.png" 
    width="150" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_pack"
/>

然后运行‘Tools/Build Bundles’（上个教程给的代码）。
查看你是否有这个新的文件。

<img 
    src="/marblestack/imgs/aa/c/check_assetbundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_assetbundles"
/>

### 步骤3️⃣

接下来就是解决文件引用的问题了。这个部分可能有点难理解而且需要重复操作。
先来看我做的图。现在看不懂没关系，等你学完这个部分就会明白了。

<img 
    src="/marblestack/imgs/aa/c/figma_diagram.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="figma_diagram"
/>

Unity的Texture引用使用的是有符号整数（可负可正）。简单来说，你可以理解成ID。我们这一步就是要修改我们生成后的AssetBundle中的ID。这样游戏才能找得到这些资源。

具体操作：

打开UABEA。打开我们刚刚打包好的AssetBundle

<img 
    src="/marblestack/imgs/aa/c/assetbundle_path.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="assetbundle_path"
/>

选择所有 SpriteAtlas 和 Sprites 并Export Dump。
把它们放在Unity里面的 My Dump 文件夹。对了，我建议你把Dumps这个文件夹也像Texture2D文件夹一样先整理一下。这样对做多个模组会有很大的帮助。

<img 
    src="/marblestack/imgs/aa/c/organize_dumps.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="organize_dumps"
/>

我们这次其实用不到Game Dump和Source Dump，因为我们将手动更改这些Text Assets。

在任意文本编辑器打开这些文件，准备下一步。

---

打开一个新的UABEA窗口，从游戏文件中找到沙包的BUN文件并打开。
在我的电脑里，该文件位置为：

```txt
"C:\Program Files (x86)\Steam\steamapps\common\Otherworld Legends\Otherworld Legends_Data\StreamingAssets\aa\StandaloneWindows64\graphiceffecttextureseparatelygroup_assets_assets\sprites\unit\unit_other_pile.psd_0678876b821c494df01ee1384bec84f2.bundle"
```

:::note
现在我画的图就能派上用场了。首先你要明白<u>黑框中的图都是在UABEA中打开的，而黑框外面的都是
我们将在 My Dump 中的需要改动的。</u>看看你能不能找得到这些文件。
:::

刚才我们Export Dump的时候包括了两种文件格式 - SpriteAtlas 和 Sprite。

1. 在SpriteAtlas这个文件的Dump里，找到`m_RenderDataMap/m_PathID`，并把它改为
和Main Texture一样的ID。（如果你看见了两个Texture2D，选不是sactx的那个）

2. 在SpriteAtlas这个文件的Dump里，找到`m_PackedSprites`（注意这是个数组，你需要
改每一个Sprite）。把它的`m_PathID`改成对应Sprite文件的ID。（注意顺序很重要！这会决定图像的动画。）
要如何知道顺序？请看`m_PackedSpriteNamesToIndex`这个地方，它其中`data`这个数是对应
Sprite的名字的，所以你的`m_PathID`要对应这些文件。

3. 现在改每一个Sprite的Dump文件。找到`m_SpriteAtlas/m_PathID`，把它改成
SpriteAtlas的ID（⚠️在目前UABEA上显示的）。

完成了这些以后，My Dump中的文件就可以完美替换源游戏文件了。

### 步骤4️⃣

接下来就和我们以前做的很像了。在UABEA里，你目前打开的就是源游戏文件所以不用打开新的。
然后做以下步骤：
1. 把sactx...这个Texture2D文件用Plugins -> Edit Texture换成Unity Texture2D里面的雕像图像。
2. 用Import Dump，把SpriteAtlas文件的Dump换成我们之前修改过的。
3. 用Import Dump，把所有Sprite文件的Dump换成我们之前修改过的。

现在我们还有一件很重要的事要完成。
用AssetStudio，打开我们的Bundle文件。然后找到开头为‘sactx’的Texture2D文件。
Export -> Selected Assets, 保存到Texture2D文件夹里。

<img 
    src="/marblestack/imgs/aa/c/save_atlas.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="save_atlas"
/>

打开UABEA，再打开游戏文件中沙包的BUN文件。用Plugins -> Edit Texture替换Main Texture(**不是sactx开头的那个**)Texture2D文件。

做完这些后运行一下基础教程的步骤五（addrtool）就大功告成了。

<img 
    src="/marblestack/imgs/aa/c/test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="test"
/>

---

本教程由Kolyn090（bilibili：木瓜凝乳蛋白酶）撰写。

<br>
<br>

💗 如果你觉得这个教程对你有帮助，可以 follow [我的 GitHub 账号](https://github.com/Kolyn090/)吗？非常感谢！

<br>
<br>

👾 Happy Gaming 👾
