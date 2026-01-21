---
title: Real-ESRGAN 动漫插图/视频修复算法
date: 2025-3-22 10:31:22
tags: ['FFmpeg', 'ACG']
categories: 图像处理
toc: true
excerpt: 介绍 Real-ESRGAN（动漫插图/视频修复算法）
---
# [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN.git)
## 动漫插图高清修复
1. Command:
```bash
./realesrgan-ncnn-vulkan.exe -i ./input/img.jpg -o ./output/img.png -n realesr-animevideov3

realesr-animevideov3 (default，针对动漫视频)
realesrgan-x4plus
realesrgan-x4plus-anime (针对动漫插画图像优化，有更小的体积)
```
2. Help:
```bash
realesrgan-ncnn-vulkan.exe -i 输入路径 -o 输出路径 [选项]...

  -h                 显示帮助信息
  -i 输入路径        图像输入路径(jpg/png/webp)或目录
  -o 输出路径        图像输出路径(jpg/png/webp)或目录
  -s 缩放比例        放大比率(可选2,3,4，默认为4)
  -t 瓦片尺寸        瓦片大小（≥32/0=自动，默认=0），对于多GPU可设置为0,0,0
  -m 模型路径        预训练模型文件夹路径，默认为models
  -n 模型名称        模型名称（默认=realesr-animevideov3，可选realesr-animevideov3 | realesrgan-x4plus | realesrgan-x4plus-anime | realesrnet-x4plus）
  -g GPU-ID         使用的GPU设备（默认自动），对于多GPU可设置为0,1,2
  -j 加载:处理:保存  各阶段线程数（默认1:2:2），对于多GPU可以调整为1:2,2,2:2
  -x                开启TTA模式
  -f 输出格式        输出图像格式(jpg/png/webp，默认根据扩展名确定为png)
  -v                 详细输出
```
## 动漫视频高清修复
1. 使用 ffmpeg 从视频中提取帧，记得提前创建文件夹tmp_frames
```bash
#ffmpeg -i onepiece_demo.mp4 -qscale:v 1 -qmin 1 -qmax 1 -vsync 0 tmp_frames/frame%08d.png
#-vsync 参数已被弃用，-vsync 0 -> -fps_mode passthrough（保持原始时间戳）
ffmpeg -i onepiece_demo.mp4 -qscale:v 1 -qmin 1 -qmax 1 -fps_mode passthrough tmp_frames/frame%08d.png
```
2. 使用 Real-ESRGAN，记得提前创建文件夹out_frames
```bash
./realesrgan-ncnn-vulkan.exe -i tmp_frames -o out_frames -n realesr-animevideov3 -s 2 -f jpg
```
3. 将增强的帧合并回视频中
```bash
#首先通过以下方式获取输入视频的 fps
ffmpeg -i onepiece_demo.mp4
#合并帧(不合并音频)
ffmpeg -r 23.98 -i out_frames/frame%08d.png -c:v libx264 -r 23.98 -pix_fmt yuv420p output.mp4
#合并帧(合并原视频音频)
ffmpeg -i out_frames/frame%08d.png -i onepiece_demo.mp4 -map 0:v:0 -map 1:a:0 -c:a copy -c:v libx264 -r 23.98 -pix_fmt yuv420p output_w_audio.mp4
```
