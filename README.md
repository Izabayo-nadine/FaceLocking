# Face Recognition (ArcFace ONNX) — 5-point

Lightweight face recognition project using an ArcFace embedder (ONNX) and simple enrollment/recognition tools.

## Overview

This repository contains scripts to detect, align, embed, enroll, and recognize faces using an ONNX ArcFace model and supporting utilities.

Key scripts (in `src/`):

- `face_locking.py` — demo/app that locks/unlocks based on face match (uses TFLite delegate in some setups).
- `enroll.py` — enroll a person from images or camera captures into the local database.
- `recognize.py` — run real-time recognition against the enrolled database.
- `embed.py`, `detect.py`, `align.py` — helper modules to produce embeddings from detected faces.
- `evaluate.py` — evaluation utilities and metrics.

## Repo layout

- `src/` — Python source files.
- `models/` — ONNX model(s) (e.g. `embedder_arcface.onnx`).
- `data/db/` — local enrollment DB (`face_db.json`, `face_db.npz`).

## Prerequisites

- Python 3.8+ recommended
- Create and activate a virtual environment:

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1    # Windows (PowerShell)
# or `source .venv/bin/activate` on Linux/macOS
```

- Install dependencies (example):

```bash
pip install -r requirements.txt
# If no requirements file exists, a typical set includes:
pip install numpy opencv-python onnxruntime pillow scipy
```

Notes:

- Some setups may require `tensorflow` or `tflite-runtime` if using the TFLite delegate shown in `face_locking.py` logs.
- If you use GPU acceleration for ONNX, install the matching `onnxruntime-gpu` package.

## Quick Start

1. Ensure `models/embedder_arcface.onnx` is present in `models/`.
2. Run enrollment (example):

```bash
python -m src.enroll --name Alice
```

3. Start recognition (camera):

```bash
python -m src.recognize
```

4. Run the face-lock demo (example):

```bash
python -m src.face_locking --name Nadine
```

During runs you will see logs about lock acquisition and similarity scores.

## Data & Models

- Enrollment database: `data/db/face_db.json` and `data/db/face_db.npz`.
- Trained embedder: `models/embedder_arcface.onnx`.

If you replace the model, ensure embedding dimensions and preprocessing match the code in `src/embed.py` and `src/align.py`.

## Tips

- Use consistent image sizes and alignment for enrollment images to improve accuracy.
- Keep the `data/db` directory backed up if you add many enrolled users.

## License

This project does not include an explicit license file. Add one if you plan to redistribute.

---

If you want, I can: generate a `requirements.txt`, add usage examples with real command-line flags, or expand the README with development and testing instructions.
