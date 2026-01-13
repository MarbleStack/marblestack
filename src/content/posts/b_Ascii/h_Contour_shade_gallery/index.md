---
title: Real ASCII Gallery - Contour Shade Filter
published: 2025-12-21
description: 'Contour Shade Filter gallery page'
image: ''
tags: [Tool, Real ASCII]
category: Tutorial
draft: false
lang: en      # Set only if the post's language differs from the site's language in `config.ts`
---

1️⃣ `cd` to `src/contour_shade`.

---

<p align="center">
    <img src="/marblestack/imgs/ba/h/gpe_colored.png" width="400">
</p>

```cmd
python contour_shade.py ^
--image_path ../../resource/imgs/girl_with_pearl_earring.jpg ^
--resize_factor 4 ^
--color_option original ^
--contrast_factor 2 ^
--thresholds_gamma 5
```

---

<p align="center">
    <img src="/marblestack/imgs/ba/h/gpe_nonfix.png" width="400">
</p>

```cmd
python contour_shade.py ^
--image_path ../../resource/imgs/girl_with_pearl_earring.jpg ^
--resize_factor 4 ^
--color_option original ^
--thresholds_gamma 4 ^
--palette_path ../../resource/palette_files/palette_default_6_arial_fast.json
```
