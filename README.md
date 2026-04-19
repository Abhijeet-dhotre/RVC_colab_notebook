<div align="center">

# 🎙️ RVC Inference — Google Colab Notebook

**Retrieval-Based Voice Conversion · No Training · No Local Uploads · 100% Google Drive**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)
[![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-CUDA%2012.1-orange?logo=pytorch)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green)](LICENSE)

</div>

---

## 📖 What Is This?

This notebook lets you **convert any voice into a trained RVC voice model** — entirely inside Google Colab, without installing anything on your computer.

**RVC (Retrieval-Based Voice Conversion)** is an AI-powered voice cloning technology. Given a trained model (`.pth` + `.index` files), it converts an input audio file so it sounds like the target voice, while preserving the original speech content.

### ✨ Key Features

| Feature | Detail |
|---------|--------|
| 🚫 No local install | Runs 100% in Google Colab |
| ☁️ Drive-first workflow | All files are read from and saved to Google Drive |
| 🎚️ Pitch control | Male→Female, Female→Male, or same-gender conversion |
| 🔊 Inline preview | Listen to the output directly in the notebook |
| 💾 Auto-save to Drive | Output is saved back to your Drive automatically |
| ⚡ Fast inference | Uses CUDA GPU + `rmvpe` pitch extraction |

---

## 📁 Google Drive Folder Structure

Before running the notebook, set up this **exact folder layout** in your Google Drive:

```
MyDrive/
└── RVC_Packages/
    ├── pth/
    │   └── YourModel.pth        ← model weights file
    ├── index/
    │   └── YourModel.index      ← index file for the model
    └── audio/
        ├── input_audio.wav      ← your source audio to convert
        └── output_audio.wav     ← created automatically after inference
```

### How to Upload Files to Drive

1. Go to [drive.google.com](https://drive.google.com)
2. Create the folder: `My Drive → RVC_Packages → pth`
3. Create the folder: `My Drive → RVC_Packages → index`
4. Create the folder: `My Drive → RVC_Packages → audio`
5. Upload your `.pth` file into the `pth/` folder
6. Upload your `.index` file into the `index/` folder
7. Upload your source audio (`.wav` / `.mp3` / `.ogg`) into the `audio/` folder

> **Tip:** Your audio file doesn't have to be named `input_audio.wav` — you can set any filename in Step 5 of the notebook.

---

## 🚀 Quick Start

### Step 1 — Open the Notebook in Colab

Upload `RVC_Inference_DriveOnly.ipynb` to Google Colab, or open it directly from your Drive.

> ⚠️ **GPU is required.** Before running any cell:  
> `Runtime → Change runtime type → Hardware accelerator → T4 GPU`

---

### Step 2 — Run Cells in Order

| # | Cell Title | What It Does |
|---|-----------|--------------|
| 1 | **Mount Google Drive** | Connects your Drive to Colab and creates the folder layout |
| 2 | **Download & Extract RVC** | Downloads the RVC runtime from Hugging Face (~once per session) |
| 3 | **Install RVC Dependencies** | Installs PyTorch (CUDA 12.1), torchcrepe, RVC packages |
| 4 | **Load Model Files from Drive** | Copies your `.pth` and `.index` from Drive to local Colab storage |
| 5 | **Load Input Audio from Drive** | Copies your audio from Drive and previews it |
| 6 | **Run Voice Conversion** | Runs inference — adjust pitch → hit Run |
| 7 | **Save Output to Drive** | Saves `output_audio.wav` back to your Drive |
| ✦ | **Download to Local Machine** | *(Optional)* Browser download of the converted file |

---

### Step 3 — Set Your File Names

In **Step 4**, update the filenames to match yours:

```python
pth_filename   = "YourModel.pth"    # ← name of your .pth file
index_filename = "YourModel.index"  # ← name of your .index file
```

In **Step 5**, set your audio filename:

```python
audio_filename = "input_audio.wav"  # ← name of your audio file
```

---

### Step 4 — Set the Pitch (Step 6)

Use the pitch slider to adjust for voice gender:

| Conversion | Recommended Pitch |
|------------|------------------|
| Male → Male | `0` |
| Female → Female | `0` |
| Female → Male | `-12` |
| Male → Female | `+12` |

---

## 🔍 Where to Get `.pth` & `.index` Model Files

You can find thousands of community-trained RVC voice models at:

> ### 🌐 [https://voice-models.com](https://voice-models.com)
>
> Browse by artist, character, language, or genre. Each model page provides both the `.pth` and `.index` files ready to download.

**Download steps:**
1. Visit [voice-models.com](https://voice-models.com)
2. Search for the voice you want
3. Download the `.pth` file → upload to `MyDrive/RVC_Packages/pth/`
4. Download the `.index` file → upload to `MyDrive/RVC_Packages/index/`

---

## ⚙️ Advanced Inference Parameters

These are set inside **Step 6** and can be changed before running:

| Parameter | Default | Description |
|-----------|---------|-------------|
| `f0_method` | `rmvpe` | Pitch extraction algorithm. Options: `rmvpe`, `pm`, `harvest` |
| `index_rate` | `0.75` | How strongly the index influences the output (0 = ignore index, 1 = full index) |
| `filter_radius` | `3` | Median filter strength on pitch curve (higher = smoother) |
| `resample_sr` | `0` | Output sample rate. `0` = keep original |
| `volume_normalization` | `0.0` | Mix ratio between input and output volume levels |
| `consonant_protection` | `0.5` | Protects unvoiced consonants from pitch conversion (0–0.5) |

---

## ❓ Troubleshooting

| Problem | Solution |
|---------|----------|
| `FileNotFoundError` on `.pth` or `.index` | Check the exact filename in Step 4 matches your Drive file |
| `FileNotFoundError` on audio | Check the filename in Step 5 and confirm it's in `RVC_Packages/audio/` |
| Inference fails with CUDA error | Go to `Runtime → Change runtime type` and select **T4 GPU** |
| Output sounds robotic | Try switching `f0_method` from `rmvpe` to `harvest` |
| Output has wrong gender tone | Adjust the `pitch` slider (±12 semitones) |
| Drive not mounting | In Step 1, click the authorization link and paste the code |

---

## 📋 Requirements

- Google account (for Google Colab + Drive)
- T4 GPU runtime (free tier on Colab)
- A trained RVC model: `.pth` + `.index` file (see [voice-models.com](https://voice-models.com))
- A source audio file (`.wav` recommended, `.mp3` / `.ogg` also work)



<div align="center">

Made with ❤️ for the RVC community

</div>
