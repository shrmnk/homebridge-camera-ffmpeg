---
title: Wyze Cam v2 / v3 / Pan / Doorbell / Outdoor
comment: on docker-wyze-bridge
author: mrlt8
date: 2021-09-29
---
**Homebridge Basic Config**

Cam V3 (max 20FPS @ 1080p):
```json
{
	"name": "CAM_NAME",
	"manufacturer": "WyzeCam",
	"model": "WYZE_CAKP2JFUS",
	"unbridge": true,
	"videoConfig": {
		"source": "-i rtsp://<docker-wyze-bridge-ip>:8554/camera-name-name",
		"vcodec": "copy"
		"maxWidth": 1920,
		"maxHeight": 1080,
		"maxFPS": 20
	}
}
```

Cam V2 (max 15FPS @ 1080p):
```json
{
	"name": "CAM_NAME",
	"manufacturer": "WyzeCam",
	"model": "WYZEC1-JZ",
	"unbridge": true,
	"videoConfig": {
		"source": "-i rtsp://<docker-wyze-bridge-ip>:8554/camera-name-cam",
		"vcodec": "copy"
		"maxWidth": 1920,
		"maxHeight": 1080,
		"maxFPS": 15
	}
}
```

If you are unsure what the maximum width, height or FPS is, you can simply omit them and let the system figure it out.

**Audio Configuration**

If you have set [`ENABLE_AUDIO` on docker-wyze-bridge](https://github.com/mrlt8/docker-wyze-bridge#audio), you can include the audio source in the `videoConfig` to feed it to Homebridge:

```json
"audio": true
```

**Doorbell Camera Configuration**

Depending on your config, you may want to rotate the doorbell cam in homebridge with hardware acceleration, which can be done by specifying your `vcodec` of choice and setting `videoFilter` to `transpose=1`:

```json
"videoConfig": {
  "source": "-i rtsp://10.0.0.10:8554/front",
  "vcodec": "libx264",
  "videoFilter": "transpose=1"
}
```

**Still Image Configuration**

If you have configured [`SNAPSHOT` on docker-wyze-bridge](https://github.com/mrlt8/docker-wyze-bridge#snapshotstill-images), you can make Homebridge make use of those still images by adding this line under `videoConfig`:

```json
"stillImageSource": "-i http://<docker-wyze-bridge-ip>:5000/snapshot/camera-name-cam.jpg"
```
