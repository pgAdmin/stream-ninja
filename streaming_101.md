# Basic Terminology

Before we talk about using `ffmpeg`, we need to understand some key terminology.


`Codec vs Container` - A codec (like H.264, AAC) is how the data is encoded. A container (like FLV, MP4, MKV) is the wrapper that holds the encoded streams together. RTMP requires FLV as the container but typically carries H.264 video and AAC audio inside.

`Bitrate` - The amount of data transmitted per second (kbps/mbps). Higher bitrate = better quality but more bandwidth. We can set this explicitly in FFmpeg with `-b:v` for video and `-b:a` for audio.

`Transcoding vs Remuxing` - Transcoding means re-encoding the media (slow, CPU-intensive). Remuxing means just changing the container without touching the streams (-c copy), which is fast and lossless.

`Stream Mapping` - When FFmpeg has multiple inputs, it uses `-map` to explicitly select which streams go into the output. Without it, FFmpeg picks automatically (usually the best video and audio stream it finds).

`Resolution & Scaling` - Common streaming resolutions are 1080p (1920×1080), 720p (1280×720), and 480p. We can scale in FFmpeg with the `-vf scale=1280:720` filter.

`Sample Rate / Channels` - Audio sample rate (typically 44100 Hz or 48000 Hz) and channel count (stereo = 2) matter for compatibility. Most platforms expect 44.1kHz or 48kHz stereo AAC.

`Keyframes / GOP` - A keyframe (I-frame) is a full image frame. Frames between keyframes (P and B frames) only store changes. GOP (Group of Pictures) is the interval between keyframes. Streaming platforms often require a fixed GOP (e.g. 2 seconds) for reliable seeking and ingest.

`Latency` - The delay between capture and playback. RTMP is a low-latency protocol, typically 2–5 seconds. Protocols like HLS have higher latency (10–30s) but better compatibility.

`Ingest vs Playback` - Ingest is the upstream from your encoder to the server. Playback is the downstream from the server to viewers. These often use different protocols — RTMP for ingest, HLS/DASH for playback.

`Stream Key` - A unique token provided by the streaming platform that identifies your stream. It's the last part of the RTMP URL and should be kept private.
