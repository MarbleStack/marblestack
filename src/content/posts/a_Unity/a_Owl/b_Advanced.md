---
title: Otherworld Legends - Advanced Modding Tutorial
published: 2025-05-15
description: 'Advanced modding tutorial for Steam game Otherworld Legends.'
image: './imgs/advance_in_game_test.png'
tags: [Game, OWL, Unity]
category: Tutorial
draft: false
lang: en      # Set only if the post's language differs from the site's language in `config.ts`
---

Please read [this tutorial](/marblestack/posts/a_unity/a_owl/a_basic/) first.

Game version used in this tutorial: v2.9.1

Windows x64

This tutorial intends to teach you how to modify game character's Spritesheet 
**so that you can edit beyond the boundary of the source Sprite.**

<img 
    src="/marblestack/imgs/aa/b/advance_in_game_test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="advance_in_game_test"
/>

(The final result you will get by the end of this tutorial)

:::important
Modding comes with unknown risks, including potential game 
instability, corrupted save files, compatibility issues, and even security 
vulnerabilities. Always back up your game files and proceed with caution.
Proceed at your own risk – I can't take responsibility if things go sideways.
:::

:::important
This is a complex tutorial. Please read and follow each step 
carefully. Send me an issue ticket if you encountered problems that you don't
understand.
:::

# Step 1️⃣

Firstly, download [Unity 2021.3.33f1](https://unity.com/releases/editor/whats-new/2021.3.33).
You won't need any Unity modules. I also strongly suggest you to learn the basics
of Unity first before proceed any further.

# Step 2️⃣

Create a new Unity Project. Choose Unity 3D as template. After you created the
project, create the following folders in Assets.

<img 
    src="/marblestack/imgs/aa/b/unity_create_project.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="unity_create_project"
/>

Inside 'Dumps', create 'Game Dump' and 'My Dump'.

<img 
    src="/marblestack/imgs/aa/b/dumps_folders.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="dumps_folders"
/>

For the purpose of teaching, this tutorial will show you how to replace the idle
state spritesheets of Quanhuying's bartender skin to the idle state spritesheet of
the Tianrendao boss. Please do bear in mind that you can definitely apply this technique with your own drawings. Using Tianrendao boss is only an example.

Their names in the spritereference folder are:

unit_asura_tianrendao.asset

unit_hero_quanhuying_bartender.asset

Use AssetStudio to extract their Texture2D files. Put them inside 'Texture2D' in Unity.

<img 
    src="/marblestack/imgs/aa/b/unity_texture2d.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="unity_texture2d"
/>

Next select those two files and make the following adjustments in the Inspector.

<img 
    src="/marblestack/imgs/aa/b/texture2d_parameter.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_parameter"
/>

Make sure:
1. Texture Type = Sprite (2D and UI)
2. Sprite Mode = Multiple
3. Mesh TYpe = Full Rect
4. Uncheck Generate Physics Shape
5. Check Read/Write
6. Filter Mode = Point(no filter)
7. Compression = None
8. Apply

Next, use AssetStudio to extract all Dump files.

<img 
    src="/marblestack/imgs/aa/b/extract_dumps.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="extract_dumps"
/>

Here are the extracted contents. Our focus is on the Sprite folder.

<img 
    src="/marblestack/imgs/aa/b/extracted_folders.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="extracted_folders"
/>

Do that for both Quanhuying bartender and Tianrendao Sprite.
You should get two Sprite folders. Here I have renamed them to
'Quanhuyin_Sprite' (spelling mistake) and 'Tianrendao_Sprite' 
and put them inside the Game Dump folder.

<img 
    src="/marblestack/imgs/aa/b/game_bundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="game_bundles"
/>

# Step 3️⃣

Next, download Unity's Sprite Editor. Open Package manager.

<img 
    src="/marblestack/imgs/aa/b/package_manager_location.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="gapackage_manager_locationme_bundles"
/>

Make sure you set Packages to Unity Registry.

<img 
    src="/marblestack/imgs/aa/b/unity_reg.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="unity_reg"
/>

Find Features -> 2D -> 2D Sprite and download that.

<img 
    src="/marblestack/imgs/aa/b/download_sprite2d.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="download_sprite2d"
/>

# Step 4️⃣

Next we will slice the Texture2D into multiple Sprites. 
Find the [BatchSpriteDumpImporter.cs](https://github.com/JianxinLin28/Otherworld-Legends-Mod/blob/main/scripts/BatchSpriteDumpImporter.cs)
script from the 'scripts' folder in this tutorial repo。

Put the csharp script (manually verified AI code✅) inside the 
Editor folder in Unity and wait for Unity to execute the code.

<img 
    src="/marblestack/imgs/aa/b/code_sprite_importer.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="code_sprite_importer"
/>

You should see a new option in the Unity menu bar called Tools.
Choose Batch Import Sprites From Dumps.

<img 
    src="/marblestack/imgs/aa/b/tools.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="tools"
/>

It will show you a popup window. Drag the Tianrendao boss Texture2D file's icon
into Target Texture, then drag Tianrendao_Sprite folder's icon to Dump Folder.
Click 'Import All Dumps'.

<img 
    src="/marblestack/imgs/aa/b/use_sprite_importer.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="use_sprite_importer"
/>

You should now see a small triangular icon next to Texture2D. If you click that
you can see all sliced Sprites.

<img 
    src="/marblestack/imgs/aa/b/sliced_tianrendao.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="sliced_tianrendao"
/>
(You can check in the Sprite Editor as well.)

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

Apply this technique on Quanhuying's bartender Texture2D as well. 

# Step 5️⃣

Next we will be editing the bartender skin (replacing the idle state to Tianrendao boss). Put the two Texture2D in any Pixel art editing software. (Here I will demonstrate using Aseprite).

It should look like this following (you will need to expand the canvas because Tianrendao boss is taller than Quanhuying)

<img 
    src="/marblestack/imgs/aa/b/draw.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="draw"
/>

Save this image.

Back to Unity, if you click the small triangular icon next to bartender's Texture2D. You
should find the first 7 sprites changed. However, we still need more adjustments.

<img 
    src="/marblestack/imgs/aa/b/texture2d_edit_mismatch.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_edit_mismatch"
/>

Now this next thing might be hard to understand. We will need to change the Sprtisheet setting for the edited Sprites. Essentially copying the settings from the original Tianrendao boss to the edited Sprites. ⚠️If you are doing your own drawings, you need to manually adjust the Spritesheet and test them so that they look right. I won't be demonstrating how to do that here. Try search how to use Sprite Editor. After you are done, go to step 6.

Create a new folder inside 'Game Dump', call it 'Temp_Sprite'. From 'Tianrendao_Sprite', copy the first seven dumps to there, and also copy from 'Quanhuyin_Sprite' (all of them except the first seven). 

<img 
    src="/marblestack/imgs/aa/b/temp_sprite.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="temp_sprite"
/>
(The red part is Tianrendao boss and the rest of them are Quanhuying)

Next, copy [RenameTextAssets.cs](https://github.com/JianxinLin28/Otherworld-Legends-Mod/blob/main/scripts/RenameTextAssets.cs) (manually verified AI code✅) from 'scripts'. After Unity executes it, you should find a new option called Rename TextAssets Window in Tools.

<img 
    src="/marblestack/imgs/aa/b/rename_text_assets.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="rename_text_assets"
/>

Next drag the first 7 dumps that belongs to Tianrendao boss to the popup window. Enter name 'unit_hero_quanhuying_bartender'. Click 'Rename Files and Update Contents'. By doing so we have renamed the files.

<img 
    src="/marblestack/imgs/aa/b/rename.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="rename"
/>

Using Batch Import Sprites From Dumps, choose Folder 'Temp_Sprite' and bartender Texture2D.

<img 
    src="/marblestack/imgs/aa/b/temp_sprite_usage.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="temp_sprite_usage"
/>

Open bartender's Sprite Editor.

<img 
    src="/marblestack/imgs/aa/b/edit_uvmap.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="edit_uvmap"
/>

Align the Spritesheet for Tianrendao and apply.

<img 
    src="/marblestack/imgs/aa/b/tianrendao_sprite_aligned.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="tianrendao_sprite_aligned"
/>

Check bartender again.

<img 
    src="/marblestack/imgs/aa/b/check_sprite.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_sprite"
/>

# Step 6️⃣

In this step we will learn how to make bundles. Select bartender Texture2D and 
find this option.

<img 
    src="/marblestack/imgs/aa/b/make_bundle.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="make_bundle"
/>

Choose 'New...', enter 'unit_hero_quanhuying_bartender'.

<img 
    src="/marblestack/imgs/aa/b/new_bundle_name.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="new_bundle_name"
/>

Find [AssetBundleBuilder.cs](https://github.com/JianxinLin28/Otherworld-Legends-Mod/blob/main/scripts/AssetBundleBuilder.cs) in scripts folder and put that in Unity Editor. After Unity executes it, you should see a new option call Build Bundles. Now select bartender Texture2D and click that option.

<img 
    src="/marblestack/imgs/aa/b/build_bundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="build_bundles"
/>

After it finishes, you will see a few new files inside 'AssetBundles'.  There is a file called 'unit_hero_quanhuying_bartender' we can open with UABEA.

<img 
    src="/marblestack/imgs/aa/b/built_bundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="built_bundles"
/>

# Step 7️⃣

Open 'unit_hero_quanhuying_bartender' inside UABEA. Choose Memory -> Info. Sort them by name.

<img 
    src="/marblestack/imgs/aa/b/my_bundle_uabea.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="my_bundle_uabea"
/>

Select the following files.
1. unit_hero_quanhuying_bartender_0
2. unit_hero_quanhuying_bartender_1
3. unit_hero_quanhuying_bartender_2
4. unit_hero_quanhuying_bartender_3
5. unit_hero_quanhuying_bartender_4
6. unit_hero_quanhuying_bartender_5
7. unit_hero_quanhuying_bartender_6

After you did that, click 'Export Dump', put them inside Unity 'Dumps/My Dump'.
Save as UABE text temp.

<img 
    src="/marblestack/imgs/aa/b/dump_from_my_bundle.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="dump_from_my_bundle"
/>

Check your 'My Dump'.

<img 
    src="/marblestack/imgs/aa/b/check_exported_my_bundle.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_exported_my_bundle"
/>

Create a new folder called 'Source Dump' inside 'Dumps'.

<img 
    src="/marblestack/imgs/aa/b/new_dump.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="new_dump"
/>

Open a new UABEA window, and from there open 'spritereference/unit_hero_quanhuyingbartender' file.
Choose an arbitrary unit_hero_quanhuying_bartender file and Export Dump into the Source Dump.

<img 
    src="/marblestack/imgs/aa/b/uabea_for_source.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="uabea_for_source"
/>

Check your 'Source Dump'.

<img 
    src="/marblestack/imgs/aa/b/check_source_dump.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_source_dump"
/>

Find [ReplacePathID38.cs](https://github.com/JianxinLin28/Otherworld-Legends-Mod/blob/main/scripts/ReplacePathID38.cs) (manually verified AI code✅) and put that
in Unity Editor folder. After Unity executes that you should see a new option called 
'Replace Line 38 From Folder'. Match 'Source Dump' and 'My Dump' and click 'Replace Line 38'.

<img 
    src="/marblestack/imgs/aa/b/replace_line38.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="replace_line38"
/>

(FYI: Line 38 in a TextAsset is the PathID of texture. We do this to change our bundle's
PathID to the source bundle's PathID.)

⚠️ After the replacement is complete. Delete all files inside 'Source Dump' to avoid bugs
next time you make mod.

# Step 8️⃣

Open a new UABEA window, and from there open 'spritereference/unit_hero_quanhuyingbartender' file.
Replace the Texture2D file. Plugins -> Edit Texture -> Ok -> Load. Select the edited Texture2D
in Unity project. Save process is the exact same as before.

Next open 'spritereference/unit_hero_quanhuyingbartender' file again. This time we want to replace
Sprtes.

Select unit_hero_quanhuying_bartender_0. Click 'Import Dump'.
Find the corresponding file in 'My Dump'.

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

Do the same with 1, 2, 3, 4, 5, 6, then apply the exact same save process.

After that, run the addrtool. Test it in the game.

<img 
    src="/marblestack/imgs/aa/b/advance_in_game_test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="advance_in_game_test"
/>

<br>
<br>

💗 If you liked this blog, consider [following me on GitHub](https://github.com/Kolyn090/).

<br>
<br>

👾 Happy Gaming 👾
