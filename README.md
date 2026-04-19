# RVC Colab Notebook

🎙️ RVC Inference — Load from Google Drive

**No training. No uploads. Just point to your Drive files and convert.**

## Required Google Drive Layout

```
MyDrive/
└── RVC_Packages/
    ├── pth/
    │   └── YourModel.pth
    ├── index/
    │   └── YourModel.index
    └── audio/
        └── input_audio.wav
```

> ⚡ Make sure you are using a **GPU runtime**:  
> `Runtime → Change runtime type → T4 GPU`

## Steps

1. **Mount Google Drive** — Connect to your Drive
2. **Download & Extract RVC** — Get the RVC runtime
3. **Install RVC Dependencies** — PyTorch, torchcrepe, etc.
4. **Load Model Files** — Copy .pth and .index from Drive
5. **Load Input Audio** — Get audio file from Drive
6. **Run Voice Conversion** — Convert with pitch adjustment
7. **Save Output** — Copy result back to Drive

## Pitch Guide

- Male→Male or Female→Female: 0
- Female→Male: -12
- Male→Female: +12

## License

MIT