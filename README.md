# qwen3-asr

![Python](https://img.shields.io/badge/Python-3.8+-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Qwen3--ASR-yellow)

A lightweight wrapper for [Qwen3-ASR](https://huggingface.co/Qwen/Qwen3-ASR-0.6B), providing a simple pipeline to transcribe audio files to text using Qwen's automatic speech recognition models. Runs in Google Colab with GPU acceleration.

## Quick Start

<a href="https://colab.research.google.com/github/wsamuelw/qwen3-asr/blob/main/qwen3-asr.ipynb" target="_blank"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a>

1. Open the notebook in Colab
2. Run all cells
3. Upload your own audio file, or use the included sample voice files (English/Chinese)
4. Get your transcription

## What It Does

Takes any audio file and converts spoken language into text transcription:

```
Audio file (.wav, .mp3, etc.)
        ↓
  Load & resample to 16kHz mono
        ↓
  Qwen3-ASR transcription
        ↓
  Text output + saved reference file
```

## Performance

Estimated transcription times on Google Colab T4 GPU (actual results may vary):

| Model | Audio Duration | Transcription Time | Device |
|-------|---------------|-------------------|--------|
| 0.6B  | 10 seconds    | ~2-4 seconds       | T4 GPU |
| 0.6B  | 1 minute      | ~8-15 seconds      | T4 GPU |
| 0.6B  | 10 minutes    | ~60-90 seconds     | T4 GPU |
| 1.7B  | 1 minute      | ~15-25 seconds     | T4 GPU |

Note: CPU transcription is significantly slower (5-10x). Performance depends on GPU type, audio length, and content complexity.

## Model Options

| Model | Size | Best For |
|-------|------|----------|
| `Qwen/Qwen3-ASR-0.6B` | 0.6B params | Fast inference, lower VRAM |
| `Qwen/Qwen3-ASR-1.7B` | 1.7B params | Higher accuracy, more VRAM |

The notebook defaults to 0.6B. Change `model_name` in Block 3 to switch.

## Requirements

- Google Colab (free tier works)
- GPU runtime recommended (`Runtime → Change runtime type → T4 GPU`)

Python dependencies (installed automatically in Colab):

```
qwen-asr
torch
torchaudio
librosa
soundfile
```

## Use Cases

- **Meeting transcription** — Record meetings and get searchable text
- **Interview processing** — Transcribe interviews for analysis
- **Content creation** — Convert podcasts/videos to written content
- **Accessibility** — Add captions or transcripts to audio content
- **Data labelling** — Bootstrap training data for NLP tasks
- **Voice notes** — Turn voice memos into written notes
- **Multi-language transcription** — Automatic language detection across 20+ languages

## How It Works

1. **Audio loading** — Uses `librosa` to resample any input audio to 16kHz mono WAV (model requirement)
2. **Model loading** — Loads Qwen3-ASR with bfloat16 precision on GPU (float32 on CPU)
3. **Transcription** — Runs `model.transcribe()` with automatic language detection
4. **Output** — Returns transcribed text and saves it to `transcription.txt`

## Key Details

- **Language detection** — Pass `language=None` for automatic detection, or specify a language code
- **Time stamps** — Set `return_time_stamps=True` in `transcribe()` for word-level timing
- **CPU fallback** — Works on CPU with float32, but significantly slower
- **Output format** — Results returned as a list; access text via `results[0].text`

## Limitations

- Requires Google Colab or a GPU environment for reasonable speed
- 0.6B model may struggle with heavy accents or background noise
- Audio must be resampled to 16kHz mono before transcription
- No streaming — full audio file required upfront

## License

Check the [Qwen3 model license](https://huggingface.co/Qwen/Qwen3-ASR-0.6B) for usage terms.
