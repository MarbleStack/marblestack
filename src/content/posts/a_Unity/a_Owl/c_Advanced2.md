---
title: Otherworld Legends - Advanced Modding Tutorial 2
published: 2025-06-02
description: 'Advanced modding tutorial 2 for Steam game Otherworld Legends.'
image: './imgs/test.png'
tags: [Game, OWL, Unity]
category: Tutorial
draft: false
lang: en      # Set only if the post's language differs from the site's language in `config.ts`
---

Please read [this tutorial](/marblestack/posts/a_unity/a_owl/a_basic/) and [this tutorial](/marblestack/posts/a_unity/a_owl/b_advanced/) first.

Game version used in this tutorial: v2.10.0

Windows x64

# This tutorial will guide you through modifying images stored in a SpriteAtlas.

<img 
    src="/marblestack/imgs/aa/c/test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="test"
/>

*(Result showcase – Sandbag)*

If you have already tried modifying most images other than character sprites using the method described in the advanced tutorial, you probably noticed that it barely works for them.  
This is because those images are packed using the **SpriteAtlas** method. A major reason is that the file references no longer match correctly.

After completing this tutorial, you should be able to modify most in-game images **without being limited by the original image size**.

:::caution
Modding may introduce unknown risks, including game instability, save corruption, compatibility issues, and even security vulnerabilities. Always back up your game files and proceed carefully.  
You assume all risks — I cannot take responsibility if problems occur.
:::

:::note
This workflow is very complex and tedious. Please read every step carefully. If you encounter problems, you can open an issue to ask for help.
:::

---

# Step 1️⃣

In this tutorial, we’ll use the sandbag in the living room as an example.  
(On my computer, its file path is:)

```txt
C:\Program Files (x86)\Steam\steamapps\common\Otherworld Legends\Otherworld Legends_Data\StreamingAssets\aa\StandaloneWindows64\graphiceffecttextureseparatelygroup_assets_assets\sprites\unit\unit_other_pile.psd_0678876b821c494df01ee1384bec84f2.bundle
```

Here is the image we want to replace it with:

<img 
    src="/marblestack/imgs/aa/c/sactx-0-128x128-BC7-unit_other_pile-1aae59fd.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="sactx-0-128x128-BC7-unit_other_pile-1aae59fd"
/>

[Credit](https://www.spriters-resource.com/pc_computer/pizzatower/sheet/193192/)

Next, open the Unity project from the advanced tutorial and locate the **Texture2D** folder.

<img 
    src="/marblestack/imgs/aa/c/texture2d_folder.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_folder"
/>

I recommend putting the previous tutorial (about the Asura boss) into a different folder. Then create a new folder, for example named **`Other_Pile`**.

Put the image you want to replace into the `Other_Pile` folder, then modify its parameters in the Inspector.

Make sure:

1. **Texture Type** = Sprite (2D and UI)  
2. **Sprite Mode** = Multiple  
3. **Mesh Type** = Full Rect  
4. **Generate Physics Shape** = Off  
5. **Read/Write** = On  
6. **Filter Mode** = Point (no filter)  
7. **Compression** = None  
8. Click **Apply**

This time, we will manually edit the spritesheet (Slice Sprites). Click **Sprite Editor**.

First is the sandbag base. Since we don’t have a base here, just draw a rectangle in any empty area.  
**Be sure to use the exact same name as shown in the example.**

<img 
    src="/marblestack/imgs/aa/c/pilebase.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="pilebase"
/>

Next is the first frame of the sandbag. Draw the rectangle over the statue on the left.  
Make sure to set the **Pivot** to **Bottom Center**.  
You can also use Custom if you know how.

<img 
    src="/marblestack/imgs/aa/c/pile0.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="pile0"
/>

There are seven more frames. Draw all of them on the statue on the right.  
Again, set the **Pivot** to **Bottom Center**.  
Name them according to the image below.

After finishing, click **Apply**. You should see the same sprites as shown in the picture.

<img 
    src="/marblestack/imgs/aa/c/pile_names.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="pile_names"
/>

---

# Step 2️⃣

In Unity **Project Settings**, find **Sprite Packer → Mode** and set it to:

> **Sprite Atlas V1 – Always Enabled**

<img 
    src="/marblestack/imgs/aa/c/proj-setting.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="proj-setting"
/>

Next, right-click in the Texture2D folder and create a **Sprite Atlas**.  
Name it: **`unit_other_pile`**

<img 
    src="/marblestack/imgs/aa/c/create_atlas.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="create_atlas"
/>

Adjust its settings:

- **Filter Mode** = Point  
- **Compression** = None  
- Drag all the sliced sprites into **Packables**  
  (⚠️ It seems you can only add them one by one, but there aren’t many, so it’s fine.)

Now the most important part — just like before, we need to build this file.

Name it:

> **`sactx-0-128x128-bc7-unit-other-pile`**

<img 
    src="/marblestack/imgs/aa/c/atlas_setting.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="atlas_setting"
/>

Also, put the original Texture2D into the atlas as well.

<img 
    src="/marblestack/imgs/aa/c/texture2d_pack.png" 
    width="150" 
    style="display:block; margin: 0 auto;"
    alt="texture2d_pack"
/>

Then run **`Tools / Build Bundles`** (the script provided in the previous tutorial).  
Check whether the new file is generated.

<img 
    src="/marblestack/imgs/aa/c/check_assetbundles.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="check_assetbundles"
/>

---

# Step 3️⃣

Next, we need to solve the **file reference problem**.  
This part can be hard to understand and requires repeated operations.

First, take a look at the diagram I made. If you don’t understand it now, that’s okay — it will make sense later.

<img 
    src="/marblestack/imgs/aa/c/figma_diagram.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="figma_diagram"
/>

Unity uses **signed integers** (can be positive or negative) as references for textures.  
You can think of them as IDs.  
Our goal is to modify the IDs inside the AssetBundle we generated so the game can correctly find these resources.

## Specific steps

Open **UABEA** and load the AssetBundle we just built.

<img 
    src="/marblestack/imgs/aa/c/assetbundle_path.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="assetbundle_path"
/>

Select all **SpriteAtlas** and **Sprite** entries and **Export Dump**.  
Put them into a folder inside Unity called **My Dump**.

I recommend organizing this Dumps folder just like the Texture2D folder. This helps a lot when working on multiple mods.

<img 
    src="/marblestack/imgs/aa/c/organize_dumps.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="organize_dumps"
/>

This time we don’t actually need **Game Dump** or **Source Dump**, because we will manually edit these text assets.

Open these dumped files in any text editor and prepare for the next step.

---

Open a new UABEA window and locate the sandbag bundle from the game files.

```txt
C:\Program Files (x86)\Steam\steamapps\common\Otherworld Legends\Otherworld Legends_Data\StreamingAssets\aa\StandaloneWindows64\graphiceffecttextureseparatelygroup_assets_assets\sprites\unit\unit_other_pile.psd_0678876b821c494df01ee1384bec84f2.bundle
```

:::note
Everything inside the black boxes in the diagram is opened in UABEA.  
Everything outside the black boxes is what you will modify in **My Dump**.
:::

When exporting dumps, you obtained two file types: **SpriteAtlas** and **Sprite**.

## Modify the dumps

1. In the **SpriteAtlas dump**, find:

`m_RenderDataMap` / `m_PathID`


Change it to match the **Main Texture ID**.  
(If there are two Texture2D entries, select the one that is NOT `sactx`.)

2. In the **SpriteAtlas dump**, find:

`m_PackedSprites`


This is an array. Modify **every Sprite entry** and change each `m_PathID` to the corresponding Sprite file ID.

⚠️ Order matters — it controls animation order.  
Check:

`m_PackedSpriteNamesToIndex`


The `data` field maps sprite names to indices. Match your `m_PathID` accordingly.

3. In each **Sprite dump**, find:

`m_SpriteAtlas` / `m_PathID`


Change it to the **SpriteAtlas ID** currently shown in UABEA.

After these edits, the files in **My Dump** are ready to replace the original game data.

---

# Step 4️⃣

This step is similar to previous workflows.

In UABEA (with the original game bundle open):

1. For the `sactx...` Texture2D, use  
**Plugins → Edit Texture** to replace it with the statue image from Unity.
2. Use **Import Dump** to replace the **SpriteAtlas** with the modified dump.
3. Use **Import Dump** to replace **all Sprite dumps** with the modified ones.

## Final texture replacement

Open **AssetStudio** and load your generated bundle.  
Find the Texture2D that starts with `sactx`.  
Choose **Export → Selected Assets**, and save it into the Texture2D folder.

<img 
    src="/marblestack/imgs/aa/c/save_atlas.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="save_atlas"
/>

Open UABEA again and load the original sandbag bundle.  
Use **Plugins → Edit Texture** to replace the **Main Texture**  

(⚠️ NOT the one starting with `sactx`).

Finally, run **Step 5 of the basic tutorial (addrtool)** — and you’re done.

<img 
    src="/marblestack/imgs/aa/c/test.png" 
    width="300" 
    style="display:block; margin: 0 auto;"
    alt="test"
/>

<br>
<br>

💗 If you liked this blog, consider [following me on GitHub](https://github.com/Kolyn090/).

<br>
<br>

👾 Happy Gaming 👾
