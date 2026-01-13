---
title: Real ASCII
published: 2025-12-11
description: 'A fast, CLI-first tool for turning images into high-fidelity ASCII art using advanced shading and edge analysis.'
image: './imgs/main_logo.png'
tags: [Tool, Real ASCII]
category: Showcase
draft: false
lang: en      # Set only if the post's language differs from the site's language in `config.ts`
---

::github{repo="Kolyn090/real-ascii"}

## ✨ Features

- 🔍️ High-resolution ASCII image conversion
- 📏 Supports variable-width (non-monospace) characters
- 🎨 Full color rendering support
- 🧵 Preserves character anti-aliasing for smoother output
- 🧩 Modular and easy to extend
- 📦 Lightweight with minimal dependencies
- 🖼️ Supports PNG / JPG
- 💻 CLI + Library usage

---

## 🖼️ Gallery (Monospace)

> Example results generated using this library.

### Original

<p align="center">
  <img src="/marblestack/imgs/ba/a/flamingo.jpg" width="200">
</p>

### Filters Preview

| Edge Trace                                                                  | Depth Shade                                                                 | Contour Shade                                                                 |
|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| <img src="/marblestack/imgs/ba/a/main_flamingo_trace.png" width="100%">       | <img src="/marblestack/imgs/ba/a/main_flamingo_shade.png" width="100%">       | <img src="/marblestack/imgs/ba/a/main_flamingo_contour.png" width="100%">       |
| <img src="/marblestack/imgs/ba/a/main_flamingo_trace_color.png" width="100%"> | <img src="/marblestack/imgs/ba/a/main_flamingo_shade_color.png" width="100%"> | <img src="/marblestack/imgs/ba/a/main_flamingo_contour_color.png" width="100%"> |

---

## 🖼️ Gallery (Non-Monospace)

> Example results generated using this library.

### Original

<p align="center">
  <img src="/marblestack/imgs/ba/a/sunflower.jpg" width="200">
</p>

### Filters Preview

| Edge Trace                                                                   | Depth Shade                                                                  | Contour Shade                                                                  |
|------------------------------------------------------------------------------|------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| <img src="/marblestack/imgs/ba/a/main_sunflower_trace.png" width="100%">       | <img src="/marblestack/imgs/ba/a/main_sunflower_shade.png" width="100%">       | <img src="/marblestack/imgs/ba/a/main_sunflower_contour.png" width="100%">       |
| <img src="/marblestack/imgs/ba/a/main_sunflower_trace_color.png" width="100%"> | <img src="/marblestack/imgs/ba/a/main_sunflower_shade_color.png" width="100%"> | <img src="/marblestack/imgs/ba/a/main_sunflower_contour_color.png" width="100%"> |

---

## 🚀 Installation

### Using Git

```bash
git clone https://github.com/Kolyn090/real-ascii.git
cd real-ascii
pip install -r requirements.txt
```

---

## 🧭 Detail

[**Edge Trace ASCII Filter**](/marblestack/posts/b_ascii/b_edge_trace/)

Edge Detection + ASCII character matching

<p align="center">
    <img src="/marblestack/imgs/ba/a/main_girl.png" width="600">
</p>

<p align="center">
    <img src="/marblestack/imgs/ba/a/main_tsunami.png" width="600">
</p>

🖼️ Go to [gallery](/marblestack/posts/b_ascii/c_edge_trace_gallery/) to see more examples!

---

[**Depth Shade ASCII Filter**](/marblestack/posts/b_ascii/e_depth_shade/)

Each shading (gradient) level has its own set of characters. Just need to 
change one value (thresholds_gamma) to make the algorithm automatically 
distinguish the gradient level for your!

<p align="center">
    <img src="/marblestack/imgs/ba/a/main_monalisa.png" width="600">
</p>

🖼️ Go to [gallery](/marblestack/posts/b_ascii/f_depth_shade_gallery/) to see more examples!

---

[**Contour Shade ASCII Filter**](/marblestack/posts/b_ascii/g_contour_shade/)

Shade around the edges.

<p align="center">
    <img src="/marblestack/imgs/ba/a/main_tsunami2.png" width="600">
</p>

🖼️ Go to [gallery](/marblestack/posts/b_ascii/h_contour_shade_gallery/) to see more examples!

---

⭐ Image Credit: 
* girl with pearl earring by Johannes Vermeer (Wikipedia)
* tsunami by hokusai (Wikipedia)
* monalisa by Leonardo da Vinci (Wikipedia)
* [flamingo](https://pin.it/N40Wiy6zx)
* [sunflower](https://pin.it/tcKqTUF4G)
