# WhisperAI-Colab
 WhisperAI-GoogleColab




---

# **Video/Audio Transcription Suite with WhisperAI** 🎙️→📝

## **Problem Statement**
Transcribing multimedia content manually is time-consuming and error-prone. Challenges include:
- Handling various audio/video formats
- Processing long-duration files
- Supporting multiple languages
- Maintaining accuracy with accents/background noise
- GPU resource requirements for AI models
- Batch processing capabilities

This solution addresses these challenges using OpenAI's WhisperAI with optimized deployment.

---

## **Key Features**
- 🔥 GPU-accelerated transcription via Google Colab
- 📁 Supports 50+ audio/video formats (MP3, WAV, MP4, MOV, AVI, etc.)
- 🌍 100+ language support
- ⚡ Multi-model selection (tiny → large)
- � Auto-format conversion & audio extraction
- 📊 Subtitle generation (SRT, VTT)
- 💾 Colab integration & cloud save options

---

## **What is WhisperAI?**
OpenAI's state-of-the-art speech recognition system trained on 680k hours of multilingual data.

### **Technical Specifications**
- **Models** (Size ⇄ Accuracy Tradeoff):
  - tiny (39M params) - Fastest
  - base (74M)
  - small (244M)
  - medium (769M)
  - large (1550M) - Most accurate

- **Input Requirements**:
  - Audio formats: WAV, MP3, FLAC, etc. (16kHz recommended)
  - Video files: Auto-converted via FFmpeg pipeline
  - Max duration: Limited by GPU memory (≈30min for large model on Colab)

- **Output**:
  - Raw text
  - Timestamps
  - Word-level confidence scores
  - Multiple subtitle formats

---


|  Size  | Parameters | English-only model | Multilingual model | Required VRAM | Relative speed |
|:------:|:----------:|:------------------:|:------------------:|:-------------:|:--------------:|
|  tiny  |    39 M    |     `tiny.en`      |       `tiny`       |     ~1 GB     |      ~10x      |
|  base  |    74 M    |     `base.en`      |       `base`       |     ~1 GB     |      ~7x       |
| small  |   244 M    |     `small.en`     |      `small`       |     ~2 GB     |      ~4x       |
| medium |   769 M    |    `medium.en`     |      `medium`      |     ~5 GB     |      ~2x       |
| large  |   1550 M   |        N/A         |      `large`       |    ~10 GB     |       1x       |
| turbo  |   809 M    |        N/A         |      `turbo`       |     ~6 GB     |      ~8x       |


[Official Repo](https://github.com/openai/whisper/blob/main/README.md)

**Why GPU?**  
Whisper uses transformer architecture - parallel computation on GPU reduces processing time by 50-100× compared to CPU.

---

## **Repo Structure**
```
WhisperAI-Colab/
├── src/
│   ├── whisper_transcriber.py      # Core processing script
│   ├── format_converter.py         # Video ⇄ audio conversion
│   └── colab_notebook.ipynb        # One-click Colab solution
├── samples/                        # Test files
├── scripts/                        # Utility scripts
├── docs/
│   ├── MODEL_COMPARISON.md         # Detailed model benchmarks
│   └── ADVANCED_SETUP.md           # Local deployment guide
└── tests/                          # Unit/integration tests
```

---

## Brands uses whisper models

- Youtube Video Transcription (Youtube Captions)

---

## **🚀 Quick Start (Google Colab)**
1. Upload then Open below jupyter notebook in your colab file
2. Run cell one-by-one

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](WhisperAI.ipynb)

---

## **⚙️ Installation** (Ignore this section if you don't want advanced usage) (just load and run jupyter notebook cells respectively)
```bash
# Clone repo
git clone https://github.com/yourusername/transcription-suite.git
cd transcription-suite

# Install dependencies
pip install -r requirements.txt

# Install FFmpeg (for video support)
sudo apt update && sudo apt install ffmpeg
```

---

## **📖 Usage** (Ignore this section if you don't want advanced usage)
```python
from src.whisper_transcriber import Transcribe

# Initialize with model selection
transcriber = Transcribe(model="large")

# Process file
result = transcriber.process_file(
    input_path="video.mp4",
    output_format="srt",
    language="auto",
    temperature=0.2
)

# Save output
result.save("transcription.srt")
```

---

## **Advanced Features**
- **Batch Processing**  
  `python src/whisper_transcriber.py --batch ./videos --model medium`

- **Subtitle Customization**  
  Adjust font, positioning, colors through SRT modification scripts

- **Language Translation**  
  Integrated with Google Translate API for multilingual support

- **Speaker Diarization**  
  (Experimental) Identify different speakers using pyannote-audio

- **Web Interface**  
  Flask-based UI for local deployment

---

## **📊 Performance Benchmarks**
![Model Comparison Chart](docs/model_speed_accuracy.png)

---

## **Limitations & Workarounds**
1. **Large File Handling**  
   Split files >30min using `scripts/split_audio.py`

2. **Background Noise**  
   Use `--noise_reduce True` flag (requires SoX)

3. **GPU Memory Errors**  
   Downgrade model size or use Colab Pro

---

## **Comparison with Alternatives**
| Feature         | WhisperAI | AWS Transcribe | Google Speech |
|-----------------|-----------|----------------|---------------|
| Cost            | Free      | $$$            | $$$           |
| Offline Use     | ✅        | ❌             | ❌            |
| Custom Models   | ❌        | ✅             | ✅            |
| Subtitle Export | ✅        | ❌             | ❌            |

---

## **FAQ**
**Q:** Can I process YouTube videos directly?  
**A:** Yes! Use various youtube downloader tools, then just pass your intended video file to this program

**Q:** How to improve accuracy for technical terms?  
**A:** Use `--initial_prompt` with domain-specific vocabulary is one of the most considerable efficient factors, however you can also read other details of whisper from it's original documentations then configure other helpful parameters

**Q:** CPU-only alternative?  (when I don't have access to any GPU)
**A:** Use tiny/base models with `--device cpu`

---

## **Contribution Guidelines**
- Report issues in GitHub tracker
- Add language packs to `src/language_profiles/`
- Benchmark tests welcome
- Follow PEP8 coding standards

---

## **License**
MIT License - Free for commercial/academic use with attribution

---
