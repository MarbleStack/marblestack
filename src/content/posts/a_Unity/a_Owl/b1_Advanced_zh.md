---
title: 战魂铭人 - 进阶模组教程
published: 2025-05-15
description: 'Steam 版本战魂铭人的>>进阶版<<模组制作教程'
image: './imgs/advance_in_game_test.png'
tags: [Game, OWL, Unity]
category: Tutorial
draft: false
lang: zh      # Set only if the post's language differs from the site's language in `config.ts`
---

在阅读本教程前，请先学习[基础教程](/marblestack/posts/a_unity/a_owl/a1_basic_zh/)。

作者：Kolyn090

教程游戏版本：v2.9.1

使用Windows x64

教程日期：5/25/2025

本教程将指引你修改游戏角色图像Spritesheet。
**这样做的目的是为了让你可以不受原贴图的大小限制修改角色皮肤。**

<img 
    src="/marblestack/imgs/aa/b/advance_in_game_test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="advance_in_game_test"
/>

（成果展示）

:::important[警告]
模组修改可能带来未知风险，包括游戏不稳定、存档损坏、兼容性问题，甚至安全漏洞。切记备份游戏文件，并谨慎操作。
风险自担——如果出现问题，我无法承担责任。
:::

:::important[警告]
该教程的操作流程非常复杂而且繁琐，请仔细阅读每一步。如果你遇到问题可以发issue提问。
:::

### 步骤1️⃣
首先，你需要[Unity 2021.3.33f1](https://unity.com/releases/editor/whats-new/2021.3.33)。
下载并安装Unity Hub，选择Unity版本2021.3.33f1。可以不装任何模组（modules）。
如果你没有使用Unity的经验，建议先观看视频学习。

### 步骤2️⃣
创建一个新的Unity项目。模板选择Unity 3D，为项目命名然后创建。
在进入Unity后，创建以下文件夹。

<img 
    src="/marblestack/imgs/aa/b/unity_create_project.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="unity_create_project"
/>


在‘Dumps’这个文件夹里面，创建两个新的文件夹。将其命名为‘Game Dump’和‘My Dump’。

<img 
    src="/marblestack/imgs/aa/b/dumps_folders.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="dumps_folders"
/>

出于教学目的，本教程仅展示将权虎鹰的马甲裙皮肤的初始状态修改为天人道boss的初始状态。
(不一定要天人道boss，你如果愿意自己画也可以但是要记得修改Spritesheet)

它们在spritereference的命名前缀为：

unit_asura_tianrendao.asset

unit_hero_quanhuying_bartender.asset

使用AssetStudio提取它们的Texture2D。并放入‘Texture2D’这个文件夹。

<img 
    src="/marblestack/imgs/aa/b/unity_texture2d.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="unity_texture2d"
/>

接下来选择这两个文件，在Inspector里面修改它们的参数。

<img 
    src="/marblestack/imgs/aa/b/texture2d_parameter.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_parameter"
/>

请确保：
1. Texture Type是Sprite(2D and UI)
2. Sprite Mode是Multiple
3. Mesh Type是Full Rect
4. 关闭Generate Physics Shape
5. 开启Read/Write
6. Filter Mode是Point(no filter)
7. Compression是None
8. 点击Apply

接下来就会比较困难了。我们先使用AssetStudio提取所有Sprite的Dump文件。

<img 
    src="/marblestack/imgs/aa/b/extract_dumps.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="extract_dumps"
/>

这是提取后的文件。我们只关心Sprite那个文件夹。

<img 
    src="/marblestack/imgs/aa/b/extracted_folders.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="extracted_folders"
/>

把两个Sprite文件夹重新取名为‘Quanhuyin_Sprite’和‘Tianrendao_Sprite’。
再把它们放到Game Dump里面。

<img 
    src="/marblestack/imgs/aa/b/game_bundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="game_bundles"
/>

### 步骤3️⃣
现在我们需要下载Unity的Sprite Editor。打开Package manager（见图）。

<img 
    src="/marblestack/imgs/aa/b/package_manager_location.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="gapackage_manager_locationme_bundles"
/>

把Packages换成Unity Registry。

<img 
    src="/marblestack/imgs/aa/b/unity_reg.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="unity_reg"
/>

找到 Features -> 2D -> 2D Sprite 并下载。

<img 
    src="/marblestack/imgs/aa/b/download_sprite2d.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="download_sprite2d"
/>

### 步骤4️⃣

接下来我们需要将切割Texture2D成多个Sprite。在本教程的scripts文件夹里面，找到

[BatchSpriteDumpImporter.cs](https://github.com/PapayaModding/Otherworld-Legends-Mod/blob/main/scripts/BatchSpriteDumpImporter.cs)。

把这个csharp代码（AI生成，已检查✅）放进Editor文件夹。放入后Unity会自动跑一下。

<img 
    src="/marblestack/imgs/aa/b/code_sprite_importer.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="code_sprite_importer"
/>

然后你的Unity上方的工具栏会多一个Tools的选项。选择Batch Import Sprites From Dumps。

<img 
    src="/marblestack/imgs/aa/b/tools.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="tools"
/>

你会看见一个弹窗，把天人道boss的Texture2D图标拖到Target Texture里面，
然后把Tianrendao_Sprite这个文件夹图标拖到Dump Folder。点击'Import All Dumps'。

<img 
    src="/marblestack/imgs/aa/b/use_sprite_importer.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="use_sprite_importer"
/>

你应该会看见Texture2D旁边有一个三角形的小图标，点开来就能看见所有Sprite。

<img 
    src="/marblestack/imgs/aa/b/sliced_tianrendao.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="sliced_tianrendao"
/>

（更直观一些，可以在Inspector里面选Sprite Editor查看。）

<img 
    src="/marblestack/imgs/aa/b/where_is_sprite_editor.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="where_is_sprite_editor"
/>

<img 
    src="/marblestack/imgs/aa/b/sprite_editor.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="sprite_editor"
/>

按照这个方法，把权虎鹰的马甲裙那份也切割一下。这里就不演示了。

### 步骤5️⃣
在这一步我们将编辑马甲裙皮肤（把初始状态换成天人道boss）。
把这两个Texture2D放进任意像素编辑软件里（不是专门像素的也行，我这里使用的是Aesprite）。

介于版权问题我就不放原画了，总之画成这个样子就行了。（因为天人道boss比较高，需要改一下图片大小）。

<img 
    src="/marblestack/imgs/aa/b/draw.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="draw"
/>

改完图片之后可以直接保存。

回到Unity，点击马甲裙的小三角图标，会发现前七个Sprites有变化。不过我们还需要调整。

<img 
    src="/marblestack/imgs/aa/b/texture2d_edit_mismatch.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_edit_mismatch"
/>


这一步可能会有些难理解。我们需要修改新图像的Spritesheet。这里要做的就是从天人道boss
的Sprite那边复制贴图变换到新的图像。⚠️如果你用的是其他的作画，你需要编辑Spritesheet然后
测试并确保贴图位置是正确的。我这里就不给与演示了。你可以搜索一下如何使用Sprite Editor。
当你完成编辑后跳到步骤六。

首先在‘Game Dump’创建一个新的文件夹，叫’Temp_Sprite‘。从’Tianrendao_Sprite‘那里复制前七个
dumps到这里，然后从’Quanhuyin_Sprite‘那里复制除了前七个所有的dumps。简单来说就是换对应的dumps。

<img 
    src="/marblestack/imgs/aa/b/temp_sprite.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="temp_sprite"
/>
（红色部分是天人道boss）


然后，在本教程的scripts里面找到[RenameTextAssets.cs](https://github.com/PapayaModding/Otherworld-Legends-Mod/blob/main/scripts/RenameTextAssets.cs)（AI生成，已检查✅），
把它放进'Editor'。Unity运行完后
你会在Tools里找到一个叫Rename TextAssets Window的新选项。

<img 
    src="/marblestack/imgs/aa/b/rename_text_assets.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="rename_text_assets"
/>

接下来把属于天人道boss的前七个dumps拖到这个弹窗里面，然后名字输入‘unit_hero_quanhuying_bartender’。
点击‘Rename Files and Update Contents’，这样文件的名字就全改好了。

<img 
    src="/marblestack/imgs/aa/b/rename.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="rename"
/>

然后用Batch Import Sprites From Dumps，文件夹选择‘Temp_Sprite’，
Texture2D选择马甲裙。

<img 
    src="/marblestack/imgs/aa/b/temp_sprite_usage.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="temp_sprite_usage"
/>

打开马甲裙的Sprite Editor。

<img 
    src="/marblestack/imgs/aa/b/edit_uvmap.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="edit_uvmap"
/>

将天人道boss的Sprite对齐。点击Apply。

<img 
    src="/marblestack/imgs/aa/b/tianrendao_sprite_aligned.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="tianrendao_sprite_aligned"
/>

再检查一下马甲裙。

<img 
    src="/marblestack/imgs/aa/b/check_sprite.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_sprite"
/>

### 步骤6️⃣
这一步我们来学习如何正确打包。选择马甲裙的Texture2D，然后找到这个选项。

<img 
    src="/marblestack/imgs/aa/b/make_bundle.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="make_bundle"
/>

选择'New...',输入‘unit_hero_quanhuying_bartender’，注意不要打错字。

<img 
    src="/marblestack/imgs/aa/b/new_bundle_name.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="new_bundle_name"
/>

在本教程的‘scripts’文件夹，找到[AssetBundleBuilder.cs](https://github.com/PapayaModding/Otherworld-Legends-Mod/blob/main/scripts/AssetBundleBuilder.cs)。
把它加到’Editor‘文件夹里面。
在Unity运行完成后，你会在Tools里看见一个叫Build Bundles的选项。选择马甲裙然后点击改选项。

<img 
    src="/marblestack/imgs/aa/b/build_bundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="build_bundles"
/>

等待运行完成后你会发现‘AssetBundles’文件夹里面多出来一些文件。其中有个叫
‘unit_hero_quanhuying_bartender’的文件我们是可以用UABEA打开的。

<img 
    src="/marblestack/imgs/aa/b/built_bundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="built_bundles"
/>

### 步骤7️⃣
在UABEA打开‘unit_hero_quanhuying_bartender’（刚刚生成的Bundle）。
选择Memory，然后Info。点击‘Name’排序一下。

<img 
    src="/marblestack/imgs/aa/b/my_bundle_uabea.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="my_bundle_uabea"
/>


接下来我想让你找到以下文件。
1. unit_hero_quanhuying_bartender_0
2. unit_hero_quanhuying_bartender_1
3. unit_hero_quanhuying_bartender_2
4. unit_hero_quanhuying_bartender_3
5. unit_hero_quanhuying_bartender_4
6. unit_hero_quanhuying_bartender_5
7. unit_hero_quanhuying_bartender_6

选择它们后，点击‘Export Dump’，把它们放在Unity里面的‘Dumps/My Dump’文件夹里面。
保存为UABE text temp。

<img 
    src="/marblestack/imgs/aa/b/dump_from_my_bundle.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="dump_from_my_bundle"
/>

检查一下‘My Dump’。

<img 
    src="/marblestack/imgs/aa/b/check_exported_my_bundle.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_exported_my_bundle"
/>

在‘Dumps'文件夹里面再创建一个叫’Source Dump‘的文件夹。

<img 
    src="/marblestack/imgs/aa/b/new_dump.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="new_dump"
/>

然后开一个新的UABEA，在里面打开‘spritereference’中的
unit_hero_quanhuying_bartender文件。就像在初始教程里做的那样。
选择七个中任意一个unit_hero_quanhuying_bartender就行，
然后也是和刚才一样Export Dump。不过这次是保存在’Source Dump‘里。

<img 
    src="/marblestack/imgs/aa/b/uabea_for_source.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="uabea_for_source"
/>

检查一下‘Source Dump’。

<img 
    src="/marblestack/imgs/aa/b/check_source_dump.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_source_dump"
/>

现在从本教程的‘scripts’里找到[ReplacePathID38.cs](https://github.com/PapayaModding/Otherworld-Legends-Mod/blob/main/scripts/ReplacePathID38.cs)(AI生成，已检查✅)
并放在Unity的'Editor‘文件夹里。
Unity运行完成后你的Tools会多一个叫’Replace Line 38 From Folder‘的选项。放入
‘Source Dump’和‘My Dump’并点击‘Replace Line 38’。

<img 
    src="/marblestack/imgs/aa/b/replace_line38.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="replace_line38"
/>

（如果你想知道什么是更换第38行：如果你打开任意一个TextAsset的话，它的第38行是材质的路径id。
这个数值在我们的打包里是随机的但是皮肤其实有一个自己的材质路径id。这是做的是替换成正确的id。）

⚠️替换完成后清空一下‘Source Dump’里的文件避免下次使用出bug。

### 步骤8️⃣
开一个新的UABEA，打开‘spritereference’里的unit_hero_quanhuying_bartender。
Memory -> Info。和初始教程一样，找到Texture2D文件，Plugins -> Edit Texture -> Ok -> Load
选择Unity里面的修改过的马甲裙Texture2D。保存步骤也和以前一样。

然后再次在UABEA打开‘spritereference’里的unit_hero_quanhuying_bartender。这次的目的是替换Sprites。
接下来这一步并不复杂但是需要重复人工操作。

找到unit_hero_quanhuying_bartender_0，然后点击‘Import Dump'。
在’My Dump‘里找到其对应的文件。

<img 
    src="/marblestack/imgs/aa/b/import_dump.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="import_dump"
/>

<img 
    src="/marblestack/imgs/aa/b/corresponding_dump.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="corresponding_dump"
/>

把1， 2， 3， 4， 5， 6的也这样做。然后还是以前的保存方法。

做完这些后运行一下基础教程的步骤五（addrtool）就大功告成了。

<img 
    src="/marblestack/imgs/aa/b/advance_in_game_test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="advance_in_game_test"
/>

---

本教程由Kolyn090（bilibili：木瓜凝乳蛋白酶）撰写。

<br>
<br>

💗 如果你觉得这个教程对你有帮助，可以 follow [我的 GitHub 账号](https://github.com/Kolyn090/)吗？非常感谢！

<br>
<br>

👾 Happy Gaming 👾
