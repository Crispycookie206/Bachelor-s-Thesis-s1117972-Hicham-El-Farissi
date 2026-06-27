# Compare Run Report

Date: 2026-03-24

This is a baseline test of smart-subsamplerv1 with COMPLEXITY_THRESHOLD set to 255, forcing all blocks into the SMOOTH path (bicubic filtering).

The custom downsampler is compared against ffmpeg in three metrics:

PSNR (Peak Signal-to-Noise Ratio), compares images pixel by pixel, calculating average squared difference from the original. Higher is better, measured in decibels.

SSIM (Structural Similarity Index), compares local patterns of luminance, contrast and structure. Measures from 0 to 1, 1 being identical.

VMAF (Video Multimethod Assessment Fusion), measure using multiple factors like detail loss, motion smoothness, and uses AI trained on how humans rate video quality.


COMPLEXITY_THRESHOLD = 255 (bicubic-only)
CHROMA MARGIN = 40
KERNEL = Mitchell-Netravali B=0, C=0.6 (matches FFmpeg default)

Input set: all images in testMaterial (Celeste, Shovel Knight, Stardew Valley, Undertale, Pixel Art Maker, Windows Desktop).

---

## Celeste

| Image             | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|-------------------|------------:|-----------:|------------:|-----------:|------------:|-----------:|
| seq1_celeste.png  |     47.7684 |    46.7129 |      0.9918 |     0.9943 |     97.3348 |    97.1202 |
| seq2_celeste.png  |     44.9011 |    45.8792 |      0.9868 |     0.9895 |     97.0914 |    97.1373 |
| seq3_celeste.png  |     47.5323 |    46.9157 |      0.9935 |     0.9941 |     97.0214 |    97.2946 |
| seq4_celeste.png  |     47.7573 |    46.4990 |      0.9926 |     0.9937 |     97.2381 |    97.1457 |
| seq5_celeste.png  |     46.9412 |    48.7376 |      0.9887 |     0.9920 |     97.5220 |    97.4368 |

## Shovel Knight

| Image                    | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|--------------------------|------------:|-----------:|------------:|-----------:|------------:|-----------:|
| seq6_shovel-of-hope.png  |     37.6919 |    37.5527 |      0.9746 |     0.9734 |     96.2906 |    96.6432 |
| seq7_shovel-of-hope.png  |     34.5946 |    34.3935 |      0.9093 |     0.9029 |     94.3541 |    95.0289 |
| seq8_shovel-of-hope.png  |     34.6216 |    34.4229 |      0.9090 |     0.9027 |     94.6167 |    95.2500 |
| seq9_shovel-of-hope.png  |     37.2567 |    37.0446 |      0.9486 |     0.9446 |     96.5469 |    96.7321 |
| seq10_shovel-of-hope.png |     34.6788 |    34.4833 |      0.9134 |     0.9070 |     94.5280 |    95.0716 |
| seq11_shovel-of-hope.png |     37.6776 |    37.5474 |      0.9746 |     0.9734 |     95.8938 |    96.3382 |
| seq12_shovel-of-hope.png |     34.7464 |    34.5306 |      0.8994 |     0.8910 |     94.5308 |    95.0559 |
| seq25_shovel-of-hope.png |     39.8585 |    39.6950 |      0.9907 |     0.9897 |     96.7140 |    96.7636 |

## Stardew Valley

| Image                     | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|---------------------------|------------:|-----------:|------------:|-----------:|------------:|-----------:|
| seq14_stardew-valley.png  |     28.9785 |    28.9416 |      0.8663 |     0.8637 |     95.1805 |    95.5313 |
| seq15_stardew-valley.png  |     41.4015 |    36.8961 |      0.9847 |     0.9606 |     97.0986 |    96.2097 |
| seq16_stardew-valley.png  |     37.7069 |    37.1710 |      0.9683 |     0.9593 |     96.0319 |    95.3222 |
| seq17_stardew-valley.png  |     36.5916 |    36.6478 |      0.9756 |     0.9797 |     96.4058 |    96.2250 |

## Undertale

| Image               | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|---------------------|------------:|-----------:|------------:|-----------:|------------:|-----------:|
| seq18_undertale.png |     55.4820 |    51.5190 |      0.9987 |     0.9968 |     97.3917 |    97.1192 |
| seq19_undertale.png |     49.0753 |    48.6242 |      0.9976 |     0.9965 |     96.9270 |    96.3076 |
| seq20_undertale.png |     48.6043 |    46.4535 |      0.9986 |     0.9968 |     96.8397 |    95.9416 |
| seq21_undertale.png |     49.0756 |    48.6245 |      0.9976 |     0.9965 |     96.9266 |    96.3071 |
| seq22_undertale.png |     50.1235 |    49.4256 |      0.9993 |     0.9988 |     95.8257 |    95.9023 |
| seq23_undertale.png |     54.0227 |    54.0585 |      0.9998 |     0.9997 |     97.4102 |    97.4111 |
| seq24_undertale.png |     48.9544 |    46.7330 |      0.9969 |     0.9939 |     96.6140 |    96.1725 |

## Pixel Art Maker

| Image                     | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|---------------------------|------------:|-----------:|------------:|-----------:|------------:|-----------:|
| seq27_pixel-art-maker.png |     33.0813 |    32.4160 |      0.9545 |     0.9541 |     95.3136 |    97.7608 |
| seq28_pixel-art-maker.png |     26.6875 |    26.7311 |      0.9013 |     0.9123 |     93.2755 |    93.8470 |
| seq29_pixel-art-maker.png |     17.7248 |    18.0675 |      0.3211 |     0.3636 |     87.2023 |   100.0000 |
| seq30_pixel-art-maker.png |     20.8079 |    22.7713 |      0.5274 |     0.5096 |    100.0000 |   100.0000 |
| seq31_pixel-art-maker.png |     27.3696 |    28.4828 |      0.7190 |     0.7051 |    100.0000 |   100.0000 |
| seq32_pixel-art-maker.png |     23.3600 |    23.4692 |      0.7344 |     0.7449 |    100.0000 |   100.0000 |
| seq33_pixel-art-maker.png |     26.9257 |    27.9610 |      0.9133 |     0.9241 |    100.0000 |   100.0000 |
| seq34_pixel-art-maker.png |      8.1259 |     8.1187 |      0.2894 |     0.2917 |      0.0000 |     0.0000 |
| seq35_pixel-art-maker.png |     13.1651 |    13.2806 |      0.3463 |     0.3489 |     85.9264 |    91.7908 |

## Windows Desktop

| Image                     | FFmpeg PSNR | Smart PSNR | FFmpeg SSIM | Smart SSIM | FFmpeg VMAF | Smart VMAF |
|---------------------------|------------:|-----------:|------------:|-----------:|------------:|-----------:|
| seq13_windows-desktop.png |     40.8480 |    41.1892 |      0.9967 |     0.9967 |     97.0282 |    96.9868 |

