# qwen3-asr

A lightweight wrapper for [Qwen3-ASR](https://huggingface.co/Qwen/Qwen3-ASR-0.6B), providing a simple pipeline to transcribe audio files to text using Qwen's automatic speech recognition models. Runs in Google Colab with GPU acceleration.

## Quick Start

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1reTM-Wo-EaqQIn2BwrDmVl93R_8HE8tU#scrollTo=QSxNjccfn3aQ)

1. Open the notebook in Colab
2. Run all cells
3. Upload an audio file when prompted
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
4. **Output** — Returns transcribed text and saves it to `reference_text.txt`

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
