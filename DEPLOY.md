# Local Development & Deployment

## Local Server (Docker)

```bash
# Start dev server (http://localhost:8080)
docker compose up

# Rebuild after dependency changes
docker compose up --build

# Stop server
docker compose down
```

## Deploy to Netlify

### Option 1: Git Push (Auto Deploy)

```bash
git add -A
git commit -m "update"
git push
```

Netlify will automatically build and deploy on push.

### Option 2: Manual Deploy (CLI)

Pre-built `_site` folder is deployed directly, skipping Netlify's build step.

```bash
# 1. Make sure local server has built _site (docker compose up)
# 2. Deploy
netlify deploy --prod --dir=_site
```

### First-time Netlify CLI Setup

```bash
npm install -g netlify-cli
netlify login
netlify link
```

## Video Conversion

Convert `.m4v` to web-friendly `.mp4`:

```bash
cd MaskAdapt/static/videos
ffmpeg -y -i INPUT.m4v -c:v libx264 -crf 28 -preset medium -an -movflags +faststart OUTPUT.mp4
```

- `-crf 28`: quality (lower = better, bigger file)
- `-an`: remove audio
- `-movflags +faststart`: enable streaming playback

Trim first N seconds:

```bash
ffmpeg -y -ss N -i INPUT.m4v -c:v libx264 -crf 28 -preset medium -an -movflags +faststart OUTPUT.mp4
```
