# Easy Streams

Here, we shall cover simple one-liners:

## Case 1: I have a short video file which containes the audio as well

```
ffmpeg -re \
    -i input.mp4 \
    -c copy \
    -f flv rtmp://your-server/live/stream-key
```

### Key flags explained:

`-re` — read input at native frame rate (essential for streaming, prevents sending faster than real-time)

`-i input.mp4` — your source video file (with audio)

`-c copy` — copy both video and audio streams without re-encoding (fast, lossless)

`-f flv` — FLV container format, required for RTMP

`rtmp://your-server/live/stream-key` — your RTMP endpoint

## Case 2: I have a separate video and audio files (all files have the same frame rate)

```
ffmpeg \
    -i video.mp4 \
    -i audio.aac \
    -c:v copy \
    -c:a aac \
    -f flv rtmp://your-server/live/stream-key
```

### Key flags explained:

`-i video.mp4 -i audio.aac` — specifies two separate input files. FFmpeg accepts multiple -i flags, each pointing to a different source.

`-c:v copy` — sets the video codec to "copy", meaning the video stream is passed through without re-encoding. Fast and lossless.

`-c:a aac` — sets the audio codec to AAC. Use this when your audio file isn't already AAC (e.g. it's MP3 or WAV). If it's already AAC, use copy instead.

`-f flv` — FLV container format, required for RTMP

`rtmp://your-server/live/stream-key` — your RTMP endpoint
