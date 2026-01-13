---
title: Real ASCII - Depth Shade Filter
published: 2025-12-19
description: 'Depth Shade Filter tutorial page'
image: ''
tags: [Tool, Real ASCII]
category: Tutorial
draft: false
lang: en      # Set only if the post's language differs from the site's language in `config.ts`
---

The shade filter renders the image with shading.
Unlike in the trace filter, where palette is optional,
shade filter requires you to set up a palette. 

## 📖 Guide: Depth Shade ASCII Art
1️⃣ `cd` to `src/depth_shade`.

2️⃣ Set up a palette. Recommended save directory is `resource/palette_files`.
Check out the [palette tutorial](/marblestack/posts/b_ascii/y_palette_tut/).

3️⃣ Execute `depth_shade.py`.
**Example**:
```cmd
python depth_shade.py --image_path ../../resource/imgs/monalisa.jpg --resize_factor 4 --invert_color
```

**Parameters**

| argument                   | help                                                                                                                                                                                                                                                                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --image_path               | The path of the image.                                                                                                                                                                                                                                              |
| --save_path                | The directory where the result image will be saved to.                                                                                                                                                                                                              |
| --resize_method            | The image resize method. Check below for available options.                                                                                                                                                                                                         |
| --resize_factor            | The resize factor of the new image.                                                                                                                                                                                                                                 |
| --contrast_factor          | The contrast factor based on the original image.                                                                                                                                                                                                                    |
| --sigma_s                  | The value of color smoothing in area.                                                                                                                                                                                                                               |
| --sigma_r                  | The value of color smoothing in edges.                                                                                                                                                                                                                              |
| --thresholds_gamma         | Controls the shading (gradient) levels. Higher value makes the algorithm emphasis the bright pixels. (Better granularity)                                                                                                                                           |
| --palette_path             | Use a palette.                                                                                                                                                                                                                                                      |
| --max_workers              | The maximum number of multithread workers.                                                                                                                                                                                                                          |
| --invert_color             | If included, invert the color of the result image.                                                                                                                                                                                                                  |
| --color_option             | The option to color the image. Check below for available options.                                                                                                                                                                                                   |
| --save_ascii               | If included, the characters will be saved to a file.                                                                                                                                                                                                                |
| --save_ascii_path          | The path to save the characters. Check out the 'ascii_output' folder for the results.                                                                                                                                                                               |
| --antialiasing             | If included, retain anti-aliasing of the characters.                                                                                                                                                                                                                |
| --reference_num            | Only used if the palette file is non-fixed width. Takes previous character as reference to replace 'filler' characters. A filler is a 1px * the row height empty character used to filling in the gaps that cannot be matched with the given characters in palette. |
| --max_num_fill_item        | Only used if the palette file is non-fixed width. This value is the maximum number of characters used to fill any gap.                                                                                                                                              |
| --filler_lambda            | Only used if the palette file is non-fixed width. Larger lambda indicates more emphasis on the gap filling with palette characters and less emphasis on the similarity between filling choices and the references.                                                  |
| --char_weight_sum_factor   | Only used if the palette file is non-fixed width. This factor indicates the importance of character weights when deciding the next character.                                                                                                                       |
| --curr_layer_weight_factor | Only used if the palette file is non-fixed width. This factor indicates the importance of a particular layer when deciding the next character. By default, we assume that the gradient image in higher index have more importance.                                  |
| --offset_mse_factor        | Only used if the palette file is non-fixed width. This factor indicates the importance of mean squared error when deciding the next character. Higher MSE means less likely to be chosen.                                                                           |
| --coherence_score_factor   | Only used if the palette file is non-fixed width. This factor indicates the importance of staying in the same level when deciding the next character.                                                                                                               |

**resize_method**

| code             | help                                          |
|------------------|-----------------------------------------------|
| nearest neighbor | Resize image with nearest neighbor algorithm. |
| bilinear         | Resize image with bilinear algorithm.         |

**color_option**

| code     | help                                                           |
|----------|----------------------------------------------------------------|
| original | Color the ASCII art with the (resized) original image's color. |

An example of ascii art image (compressed):

<p align="center">
    <img src="/marblestack/imgs/ba/e/shade_monalisa.png" width="400">
</p>

---

🖼️ Also check out the [gallery](/marblestack/posts/b_ascii/f_depth_shade_gallery/) for more examples!

---

⭐ Image Credit: monalisa (Wikipedia)

<p align="center">
    <img src="/marblestack/imgs/ba/e/monalisa.jpg" width="400">
</p>
