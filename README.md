# `whisper-asr-webapp`

[![Docker](https://github.com/FluxCapacitor2/whisper-asr-webapp/actions/workflows/docker.yml/badge.svg)](https://github.com/FluxCapacitor2/whisper-asr-webapp/actions/workflows/docker.yml)
![GitHub last commit (branch)](https://img.shields.io/github/last-commit/FluxCapacitor2/whisper-asr-webapp/main)

A web app for automatic speech recognition using OpenAI's Whisper model running locally.

```sh
# Quickstart with Docker:
docker run --rm -it -p 8000:8000 -v whisper_models:/root/.cache/whisper ghcr.io/fluxcapacitor2/whisper-asr-webapp:main
```

![](/.github/readme_images/app_dark.png#gh-dark-mode-only)
![](/.github/readme_images/app_light.png#gh-light-mode-only)

## Features

- Customize the model, language, and initial prompt
- Enable per-word timestamps (visible in downloaded JSON output)
- Runs Whisper locally
- Pre-packaged into a single Docker image
- View timestamped transcripts in the app
- Download transcripts in plain text, VTT, SRT, TSV, or JSON formats

## Architecture

The frontend is built with Svelte and builds to static HTML, CSS, and JS.

The backend is built with FastAPI. The main endpoint, `/transcribe`, pipes an uploaded file into ffmpeg, then into Whisper. Once transcription is complete, it's returned as a JSON payload.

In a containerized environment, the static assets from the frontend build are served by the same FastAPI (Uvicorn) server that handles transcription.

## Running

1. Pull and run the image with Docker.
   - Run in an interactive terminal: `docker run --rm -it -p 8000:8000 -v whisper_models:/root/.cache/whisper ghcr.io/fluxcapacitor2/whisper-asr-webapp:main`
   - Run in the background: `docker run -d -p 8000:8000 -v whisper_models:/root/.cache/whisper ghcr.io/fluxcapacitor2/whisper-asr-webapp:main`
2. Visit http://localhost:8000 in a web browser
