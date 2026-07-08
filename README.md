# SETU — Indian Sign Language Communication System

**SETU** (meaning *bridge* in Sanskrit) is a fully offline Text-to-Sign Language system that converts English text into Indian Sign Language (ISL) video clips in real time.

Built to bridge communication between hearing and deaf/hard-of-hearing communities.

---

## What it does

Takes an English sentence as input, applies ISL grammar rules, and plays the corresponding ISL sign video clips — fully offline, no internet needed.

**Example:** 
Input: "I want to eat food tomorrow" 
Output: ISL signs played in correct order: TOMORROW I FOOD EAT WANT 

---

## How it works 

Text Input -> ISL Grammar Reordering -> Clip Lookup -> Video Playback

1. **ISL Grammar Reordering** — English follows Subject-Verb-Object order. ISL follows Time-Topic-Comment order. spaCy is used to reorder words into correct ISL buckets: `TIME → GREETINGS → PRONOUN → NOUN → VERB → OBJECT → NEGATION → QUESTION`

2. **Clip Lookup** — Searches 9,327 ISLRTC video clips using a fast dictionary index. Handles plurals, -ing forms, and word mappings automatically.

3. **Smooth Playback** — Plays clips in a single persistent OpenCV window with a progress bar. Uses INTER_AREA interpolation for clean resizing.

---

## Results

- 9,327 ISL clips from ISLRTC dictionary
- 97.96% sentence coverage
- Fully offline — no internet or cloud needed
- Runs on CPU, no GPU required

---

## Tech Stack

- Python 3.12
- spaCy (ISL grammar reordering)
- OpenCV (video playback)
- NumPy

---

## Clip Database

Clips are sourced from the **ISLRTC (Indian Sign Language Research and Training Centre)** official dictionary — 9,327 clips organized A-Z by word.

Due to size (several GB), clips are not included in this repository.

Download from: [ISLRTC Google Drive](https://islrtc.nic.in)

Place extracted clips at:
```
data/
└── isl_clips/
    ├── A/
    ├── B/
    ├── ...
    └── Numbers/
```

---

## Notebooks

| Notebook | Description |
|---|---|
| `1_keypoint-detection.ipynb` | MediaPipe keypoint extraction experiments |
| `2_text-to-sign.ipynb` | Main Direction B pipeline — Text to ISL Sign |
| `3_direction_a_final.ipynb` | Sign recognition model (INCLUDE ISL dataset) |

---

## Project Context

Built as part of **SETU** — a bidirectional ISL communication system for the deaf community.

- **Direction B (this repo):** Text → ISL Signs ✅
- **Direction A (collaborator):** ISL Signs → Text (in progress)
- **Speech to Sign:** Converting speech input to ISL signs (in progress)

---

## How to Run

1. Clone the repository
```bash
git clone https://github.com/YShamili/SETU-ISL.git
cd SETU-ISL
```

2. Install dependencies
```bash
pip install opencv-python numpy spacy
python -m spacy download en_core_web_sm
```

3. Download ISLRTC clips and place at `data/isl_clips/`

4. Open `notebooks/2_text-to-sign.ipynb` in Jupyter

5. Run all cells — then call:
```python
text_to_sign_smooth("your sentence here")
```

---

## Author

**YShamili** — CSE Student, IIT Hyderabad  
Built for real-world assistive technology impact.
