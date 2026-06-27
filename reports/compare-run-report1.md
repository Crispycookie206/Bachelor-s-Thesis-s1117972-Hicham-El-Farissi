# Compare Run Report

Date: 2026-03-24

This is a base test of the crude implementation of smart-subsamplerv1 with generic ffmpeg downsampling pipelines. The smart subsampler is compared against ffmpeg in three metrics:

PSNR (Peak Signal-to-Noise Ratio), compares images pixel by pixel, calculating average squared difference from the original. Higher is better, measured in decibels.

SSIM (Structural Similarity Index), compares local patterns of luminance, contrast and structure. Measures from 0 to 1, 1 being identical.

VMAF (Video Multimethod Assessment Fusion), measure using multiple factors like detail loss, motion smoothness, and uses AI trained on how humans rate video quality.

COMPLEXITY THRESHOLD = 10
CHROMA MARGIN = 40



Input set: all Pixel Art Maker images from testMaterial.

| Image                      | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|----------------------------|-------------|------------|-------------|------------|-------------|------------|
| seq27_pixel-art-maker.png  |     33.0813 |    32.4160 |      0.9545 |     0.9541 |     95.3136 |    97.7608 |
| seq28_pixel-art-maker.png  |     26.6875 |    25.5825 |      0.9013 |     0.9633 |     93.2755 |    83.4673 |
| seq29_pixel-art-maker.png  |     17.7248 |    15.4132 |      0.3211 |     0.7295 |     87.2023 |   100.0000 |
| seq30_pixel-art-maker.png  |     20.8079 |    24.7402 |      0.5274 |     0.5650 |    100.0000 |   100.0000 |
| seq31_pixel-art-maker.png  |     27.3696 |    28.4828 |      0.7190 |     0.7051 |    100.0000 |   100.0000 |
| seq32_pixel-art-maker.png  |     23.3600 |    21.1539 |      0.7344 |     0.8521 |    100.0000 |   100.0000 |
| seq33_pixel-art-maker.png  |     26.9257 |    26.7495 |      0.9133 |     0.9533 |    100.0000 |   100.0000 |
| seq34_pixel-art-maker.png  |      8.1259 |     8.1187 |      0.2894 |     0.2917 |      0.0000 |     0.0000 |
| seq35_pixel-art-maker.png  |     13.1651 |    13.2451 |      0.3463 |     0.3485 |     85.9264 |    97.1249 |

## One Image Per Game

Input set: one representative image from each game (Celeste, Shovel of Hope, Stardew Valley, and Undertale).

| Image                      | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|----------------------------|-------------|------------|-------------|------------|-------------|------------|
| seq1_celeste.png           |     47.7684 |    46.7129 |      0.9918 |     0.9943 |     97.3348 |    97.1202 |
| seq6_shovel-of-hope.png    |     37.6919 |    36.6030 |      0.9746 |     0.9776 |     96.2906 |    95.9693 |
| seq14_stardew-valley.png   |     28.9785 |    28.6950 |      0.8663 |     0.8758 |     95.1805 |    93.5855 |
| seq18_undertale.png        |     55.4820 |    51.5190 |      0.9987 |     0.9968 |     97.3917 |    97.1192 |

## Generated Files

- ffmpeg-output/<testName>-ffmpeg-output.png
- smart-output/<testName>-smart-output.png

## Results analysis

Even though the smart subsampler is currently in an incomplete state, and untuned, I can use these results to make some observations about the base properties of both pipelines:

The near identical PSNR scores tell me that both ffmpeg and the smart implementation hit the same quality ceiling when it comes to information loss at the pixel level.

Nevertheless, when it comes to retaining the overal structure of the image, my implementation shows clear improvements with semi-consistently higher SSIM scores. While relatively small, it shows there is still potential for improvement. 

I have also realized that the patterns vmaf recognizes as good are a bit hit or miss, so its really unstable and hard to interpret the vmaf results at the worst case tests. vmaf might see the hard chroma shifts my algorithm chooses as unnatural and penalize the score.

My algorithm currently makes more mistakes in raw pixel values, but preserves structure better, which is the intended effect I was striving for, but noticeably in the real world example tests, the scores are already so high, that differences are minute and inconsistent. Stardew Valley yielded abnormally lower scores, which might have to do with the scaling of in game pixels being unalligned with 2x2 block grids.



An important note: I suspect the high scores for real world images are caused by the high resolution of the test material, where edge smears get drowned out and not reflected well in the scores. The low effect of my logic method might be due to:

    - Many screenshots are already upscaled from a lower internal resolution, so one game pixel spans multiple real pixels. Bigger color blocks scores don't suffer as much from that edge chroma bleed

    - 4:2:0 removes chroma detail, while perceived sharpness is dominated by luma. So edges can still look sharp even if color is bleeding slightly.

    - 4:2:0 works on 2x2 chroma neighborhoods. If edges align with that grid, then the edge will be represented perfectly anyways, so there isn't room for inprovement in that case. Stardew valley might be the only exception which is why I think the scores were much lower there.
