---
title: TP-Link NC200 and NC220
author: shrmnk
date: 2022-09-24
---
**Homebridge Config**

```json
{
  "name": "Camera",
  "manufacturer": "TP-Link",
  "model": "NC220",
  "unbridge": true,
  "videoConfig": {
      "source": "-i rtsp://USERNAME:PASSWORD@CAMERA-IP-OR-HOST:554/h264_vga.sdp",
      "maxWidth": 640,
      "maxHeight": 480,
      "maxFPS": 20,
      "vcodec": "h264_omx",
      "audio": false
  }
}
```

**Additional Information**

I achieved the best best quality and least interruptions with the following settings:

- set the FPS in the camerca config UI to 20 FPS, more FPS lead to interruptions (but YMMV!)

- h264_omx gives the best performance on Raspberry Pis with small quality impact. On non-Pis, you'll probably want to choose another codec

- No audio is available with this stream, I haven't figured out how to get it working
