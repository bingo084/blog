---
title: 使用 WebP 加速网站
date: 2024-04-15T16:44:15+08:00
draft: false
type: posts
keywords:
tags:
  - webp
categories:
  - web
resources:
  - name: featured-image
    src: images/featured-image.webp
---

[WebP] 是 Google 开发的一种光栅图形文件格式，旨在替代 JPEG、PNG 和 GIF 文件格式。
它支持有损和无损压缩，以及动画和 Alpha 透明度。

<!--more-->

## 为什么要使用 WebP

> WebP 是一种现代图片格式，可为网络上的图片提供出色的无损和有损压缩。
> 使用 WebP，网站站长和 Web 开发者可以创建更小、更丰富的图片，从而提高网页加载速度。
>
> 与 PNG 相比，WebP 无损图片的尺寸缩小了 26%。WebP 有损图片比采用等效 SSIM 质量指数的同等 JPEG 图片小 25-34%。
>
> 无损 WebP 支持透明度（也称为 Alpha 通道），但只需额外增加 22% 的字节。
> 对于可以接受有损 RGB 压缩的情况，有损 WebP 也支持透明度，其文件大小通常比 PNG 小 3 倍。
>
> 动画 WebP 图片支持有损、无损和透明度，与 GIF 和 APNG 相比，此类图片可缩减大小。

## 体验 WebP

[WebP - 图片格式的发展趋势](https://www.upyun.com/webp)

可以看到，在图片尺寸大幅下降的同时，图片质量并没有明显下降。
这可以极大加速网站的加载，减小流量消耗，提升用户体验。

## 使用 WebP

有许多在线网站可以将图片转换为 WebP 格式，也有离线转换工具。
常见的离线转换工具有 [Cwebp]

```bash { title = "Cwebp 使用示例" }
cwebp -q 50 -lossless picture.png -o picture_lossless.webp
cwebp -q 70 picture_with_alpha.png -o picture_with_alpha.webp
cwebp -sns 70 -f 50 -size 60000 picture.png -o picture.webp
cwebp -o picture.webp -- ---picture.png
```

## 效果

我把博客中较大的封面图都转换成了 WebP 格式，使用 [Google PageSpeed Insights] 测试了一下。

[优化前]只有 69 分，[优化后]达到了 92 分。

[WebP]: https://developers.google.com/speed/webp?hl=zh-cn
[Cwebp]: https://developers.google.com/speed/webp/docs/cwebp?hl=zh-cn
[Google PageSpeed Insights]: https://pagespeed.web.dev/
[优化前]: https://pagespeed.web.dev/analysis/https-binlog-cc/e2s9e1c42a?form_factor=desktop
[优化后]: https://pagespeed.web.dev/analysis/https-binlog-cc/z7h36r6x7k?form_factor=desktop
