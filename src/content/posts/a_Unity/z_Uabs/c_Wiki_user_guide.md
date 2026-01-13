---
title: UABS Wiki - User Guide
published: 2025-07-23
description: 'User Guide for UABS'
image: ''
tags: [Game, Unity, UABS]
category: Tutorial
draft: false
lang: en      # Set only if the post's language differs from the site's language in `config.ts`
---

::github{repo="PapayaModding/UABS"}

<p align="center">
    <img src="/marblestack/imgs/az/a/logo.png" width="300"/>
</p>

Tutorial version [v1.0.3-Beta](https://github.com/Kolyn090/UABS/releases/tag/v1.0.3-beta).

⛳ Note: I have renamed manual cache to user package after v1.0.3-Beta. If you are working with another version you should refer 'Cache' as
'Package'. 

# 📘 User Guide

Welcome to the **UABS User Guide**. This guide walks you through how to use the tool—from launching it for the first time to performing advanced tasks.

❗Modding can be complex, which is why the design of UABS might not feel intuitive at first. Please read this User Guide carefully to understand what the tool can and cannot do.

---

## 🧭 Table of Contents

1. [Getting Started](#getting-started)
2. [User Interface Overview](#user-interface-overview)
3. [Opening a Bundle File](#opening-a-bundle-file)
4. [Building Manual Cache](#building-manual-cache)
5. [Searching for Bundles](#searching-for-bundles)
6. [Viewing and Exporting](#viewing-and-exporting)
7. [Asset Memo](#asset-memo)
8. [Dependency Navigation](#dependency-navigation)
9. [Troubleshooting](#troubleshooting)

<br>

<a name="getting-started"></a>
## 🟢 Getting Started

1. Download the any release from the [Releases](https://github.com/Kolyn090/UABS/releases) page.
2. Launch the standalone `.exe` or open the Unity project if you're using the dev version.


<img width="700" alt="getting-started1" src="https://github.com/user-attachments/assets/7f216209-d70f-4537-905f-6f942ab395de" />


> 💡 **Special Note:** UABS works best with Unity 2021.3.33f1 bundles.

<br>

<a name="user-interface-overview"></a>
## 🖥️ User Interface Overview

| Option | Note |
| --- | --- |
| File | - 📄Open File: open a file in UABS (only ".bundle", ".ab", ".assets" files are included) <br>- 📁Open Folder: open a folder and search for files described above. |
| Export | - 🌌Export All: export all assets in a bundle. (currently only support images)<br>- 👆Export Selected: export all selected assets in a bundle. (currently only support images)<br>- 🧱Export Filtered: export all filtered assets in a bundle. (currently only support images) <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ only works in a Bundle. |
| Search | - 🔑By Keywords: find all bundles that contain any of the keywords in their names, or if any of their assets contain any of the keywords in their names. The keywords are separated by a comma. For example: hero,weapon,skill. If you specify exclude keywords and a match includes any of the exclude keywords, it won't be included in the final result. <br>- 🖼️By Image: use a Sprite / Texture2D to search the Bundle(s). The actual comparison is done with name, not pixels. <br>- 📝By Memo: very similar to 'By Keywords' but instead of name it searches asset memo. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ you will need to build a manual cache first before using this feature.|
| Dependency | - 🧩Search Bundle's dependencies: the dependency bundles will be displayed as a folder view. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ you will need to build a manual cache first before using this feature. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ only works in a Bundle. |
| Filter | - 🧱Filter assets in a bundle by asset type (AssetClassID). <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ only works in a Bundle. |
| Memo | - 📂Select Memo Cache: specify a manual cache for memo storage. <br>- 🧬Inherit Memo: transfer memo from older game versions to a newer version. It has three modes: <br>&nbsp;&nbsp;&nbsp;&nbsp;* Safe: do not transfer memo if the memo field in the current version is non-empty. <br>&nbsp;&nbsp;&nbsp;&nbsp;* Overwrite: transfer all memo from the older version if its memos field is non-empty. <br>&nbsp;&nbsp;&nbsp;&nbsp;* Force: transfer all memos whenever there is a match. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⚠️ you will need to build a manual cache first before using this feature.|
| Cache (manual cache) | - 🗃️Build New Cache: click button 'Build New Cache' to build a new cache. Select the game data folder, such as StreamingAssets(PC), split_UnityDataAssetPack(Android). After that, create a new folder under UABS_Cache (by you) and select it. Wait for the process to complete (the entry in scrollview will turn from gray to white). <br>- 🗑️Remove Cache: click the 'X' button to remove an existing cache. |
| Back | - ↩️To go back: click this button to go back. If you are in a bundle, it will go back to its folder. If you are in a folder, it will go to its parent folder. If you are in dependency / search view, it will go to the last view. |

<br>

<a name="opening-a-bundle-file"></a>
## 📂 Opening a Bundle File
In the toolbar, hover over 'File' option and select 'Open File'.

<img width="700" alt="opening-a-bundle1" src="https://github.com/user-attachments/assets/e2a67849-bfc9-431a-a757-d8ecbe7258a4" />

Open a file that has extension "bundle".

<img width="788" height="280" alt="opening-a-bundle2" src="https://github.com/user-attachments/assets/8a80d327-3c37-46f6-93ce-307ca4c6b368" />

There you go!

<img width="700" alt="opening-a-bundle3" src="https://github.com/user-attachments/assets/a09e554e-a445-405e-9345-fa30d3084e64" />


> ⚠️ **Special Notice:** Large files may take time to load due to current I/O limitations.

<br>

<a name="building-manual-cache"></a>
## 🗃️ Building Manual Cache
Select 'Cache' -> 'Build New Cache' -> 'Build New Cache'.

<img width="700" alt="building-manual-cache1" src="https://github.com/user-attachments/assets/ebfbe508-5a24-45fc-b5ea-c45064e4b3c4" />

Select the game data folder. 

> If it's a Windows Steam game, the directory is usually '~/steamapps/common/[GAME]/[GAME]_Data/StreamingAssts/aa/StandaloneWindows64'. 

> For Android APK, it's '~/split_UnityDataAssetPack/assets/aa/Android'.

<img width="229"  alt="building-manual-cache2" src="https://github.com/user-attachments/assets/09bfc403-bd2f-46cd-8cb1-1433c2e5e6cc" />

After choose the game data folder, create a new folder under 'UABS_Cache' (by you) and select it. I recommend you to name the folder like so: [GAME]-[VERSION]. For example, if you game is called "OWL" and version is "2.11.0.2", do:

<img width="742" alt="building-manual-cache3" src="https://github.com/user-attachments/assets/67f7d0cf-ab87-4cd7-a208-1da72e968add" />

Go to 'Build New Cache' panel again and you shall see a new entry that has background color of gray. This mean that UABS is still processing the game data folder.

<img width="231" height="185" alt="building-manual-cache4" src="https://github.com/user-attachments/assets/cc223746-f1a2-445a-bd7d-41cdf112cfbb" />

After UABS is done, the background color should turn white, as shown in this image:

<img width="232" height="185" alt="building-manual-cache5" src="https://github.com/user-attachments/assets/832475cb-b8f9-42af-bb5c-6f8a8f160f3f" />

🎉 Now you have your very first manual cache! This is going to be necessary for many features provided by UABS.

<br>

<a name="searching-for-bundles"></a>
## 🔍 Searching for Bundles

You can search bundles in UABS. For example, by keywords. Go to 'Search' -> 'By Keywords' -> Select a cache in the scrollview.

<img width="700" alt="searching-for-bundles1" src="https://github.com/user-attachments/assets/8ff0bc21-ea00-46d0-be53-c274054cbc6c" />

After you have selected the cache, its background should turn white.

<img width="224" height="93" alt="searching-for-bundles2" src="https://github.com/user-attachments/assets/10bbc65b-5fc5-472e-9146-420bc8aa04fa" />

Now follow the guideline and enter your keywords (and exclude keywords, if any). After you are done, click 'Search'.

<img width="225" height="223" alt="searching-for-bundles3" src="https://github.com/user-attachments/assets/21b094fc-ab86-4529-b896-ec532ab6b119" />

If any match result is found, it will display them.

<img width="700" alt="searching-for-bundles4" src="https://github.com/user-attachments/assets/73093a6d-e74c-4bd9-9125-3a70de75f979" />


<br>

<a name="viewing-and-exporting"></a>
## 🖼️ Viewing and Exporting Assets

**Currently, UABS only supports viewing and exporting Sprite & Texture2D assets.**

To view the file, click on the asset entry. The display panel will show the asset if it's supported by UABS. You can zoom and pan images.

<img width="700" alt="viewing-and-exporting1" src="https://github.com/user-attachments/assets/9906ca37-45ff-4254-afac-a2855728dc3b" />

To export assets, go to 'Export' -> 'Export all assets'. Select a place to save.

<img width="700" alt="viewing-and-exporting2" src="https://github.com/user-attachments/assets/99a230cb-e7d2-47a0-881b-e9b24ee29ab8" />

After you open the export folder, you should see folders like the following.

<img width="322" height="143" alt="viewing-and-exporting3" src="https://github.com/user-attachments/assets/bfa9fc0d-d849-47bc-9d9c-a486e392f059" />

<br>

<a name="asset-memo"></a>
## 🏷️ Asset Memo

You can use the memo feature for quick navigation, annotation, or project organization. But first of all, you need to enable it. To do that, go to 'Memo' -> 'Select Memo Cache' -> Select a cache for storing memo. You should also expect the cache entry to turn white after you click it.

<img width="700" alt="asset-memo1" src="https://github.com/user-attachments/assets/2f4cfd42-c8d1-4e80-9d69-43346f51404e" />

The memo field should become available after you do that. (Notice currently only Sprite & Texture2D assets work, for other kinds of assets the field should still be disabled)

<img width="321" height="187" alt="asset-memo2" src="https://github.com/user-attachments/assets/b5f92292-74a1-47dd-9a84-6b36cd3263e6" />

You can type in memo field like so:

<img width="321" height="194" alt="asset-memo3" src="https://github.com/user-attachments/assets/af74bba2-6bec-4997-a44e-05c7fdb8aade" />

🎉 Now there is your first memo in UABS!

Let's apply search again but with memo this time. This time, go to 'Search' -> 'By Memo'. Select the cache. Enter your search keyword to find the assets you memo. You don't need to search exactly. For example, if your memo was "
Harry Potter and the Chamber of Secrets", searching "Harry Potter" will match them just fine.

<br>

<a name="dependency-navigation"></a>
## 🔗 Dependency Navigation

UABS treats dependency differently from other tools. You can actually navigate to a dependency bundle and find its dependency from there! It's very easy to do in UABS. Go to 'Depend' -> Select a cache entry in the scrollview.

<img width="700" alt="dependency-navigation1" src="https://github.com/user-attachments/assets/a81dc627-fa85-49f3-85b8-b78e49c2f159" />

It will automatically search all dependency bundles for you. Here are the dependencies for my current bundle.

<img width="700" alt="dependency-navigation2" src="https://github.com/user-attachments/assets/5e32538c-09fd-43b9-a81d-67559d57de62" />


<br>

<a name="troubleshooting"></a>
## 🧯 Troubleshooting

UABS is not well tested, encountering problems is normal. If you did, please go to C:\Users\[YOUR USER NAME]\AppData\LocalLow\DefaultCompany\UABS and find Player.txt. Open an issue and send that to me. Tell me how to replicate the situation so that I can investigate. 

<br>

## 🙏 Thanks for using UABS!

If you like this project, please consider giving my repo a ⭐!

Feel free to explore the other wiki pages for more details.
