---
title: "TIL ffmpeg vágás, fájlméret csötkkentés"
tags: 
- TIL
- ffmpeg
- CLI
- video
---

Nyilván van mindenféle hasznos video vágó szoftver, akár ingyen is, de a legjobb a parancssor.

Videot vágni `ffmpeg`gel ennyire könnyü:

```bash
ffmpeg -i INPUT_VIDEO.mp4 -ss hh:mm:ss.xxx -to hh:mm:ss.xxx -c copy OUTPUT_VIDEO.mp4
```

Ha pedig (valószínűleg) H.264 codec-kel volt kódolva, azt H.265-ösre átkód(ek)olva nagymértékben  csökkenthető a fájlméret, juhé:

```bash
ffmpeg -i INPUT_VIDEO.mp4 -vcodec libx255 -crf 27 OUTPUT_VIDEO.mp4
```
(A `-crf` után a minőségi beállíásokhoz [RTFM](https://trac.ffmpeg.org/wiki/Encode/H.264))