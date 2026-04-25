# RapidMaia-GM

RapidMaia-GM is a Maia-style neural chess engine trained on high-level rapid games (≥2400) to model **2600-level human decision-making**.

Unlike traditional engines such as Stockfish, this project prioritises **realistic human play** over perfect accuracy.

---

## 🎯 Objectives

* Model grandmaster-level rapid play (5–15 min)
* Produce human-like decisions, not engine-perfect moves
* Maintain realistic variability and uncertainty
* Avoid brute-force search as the primary strength mechanism

---

## 📁 Repository Structure

RapidMaia-GM/
│
├── README.md
├── requirements.txt
├── setup.py
├── .gitignore
│
├── configs/
│   └── train.yaml
│
├── data/
│   ├── download.py
│   ├── preprocess.py
│   └── filters.py
│
├── models/
│   ├── model.py
│   ├── layers.py
│   └── encoding.py
│
├── training/
│   ├── train.py
│   ├── dataset.py
│   └── loss.py
│
├── evaluation/
│   ├── metrics.py
│   ├── stockfish_eval.py
│   └── benchmark.py
│
├── inference/
│   ├── play.py
│   ├── sampling.py
│   └── engine.py
│
├── utils/
│   ├── logging.py
│   └── helpers.py
│
├── notebooks/
│   └── exploration.ipynb
│
└── checkpoints/

---

## 📊 Dataset

Uses Hugging Face dataset:

from datasets import load_dataset
ds = load_dataset("angeluriot/chess_games")

### Filtering

* Rating ≥ 2400
* Time control: rapid only (5–15 min)
* Remove low-quality/blunder-heavy samples where possible

---

## 🧠 Model

* Convolutional Neural Network (CNN)
* Residual blocks
* Policy head (move probabilities)

### Inputs

* Board representation
* Side to move

### Outputs

* Probability distribution over legal moves

---

## 🏋️ Training

* Supervised learning
* Objective: predict human moves
* Loss: cross-entropy + label smoothing

---

## 🎮 Inference (Human Behaviour)

probs = softmax(logits / T)  (T ≈ 0.8–1.0)
probs = 0.9 * probs + 0.1 * noise
move = sample(probs)

This ensures:

* non-deterministic play
* realistic variation
* human-like uncertainty

---

## 📈 Evaluation

Tracked using Weights & Biases.

### Imitation

* Top-1 / Top-3 / Top-5 accuracy

### Strength

* Average centipawn loss
* Blunder rate (>200cp)
* Engine agreement

### Behaviour

* Entropy (uncertainty)
* Top-1 vs Top-2 probability gap

---

## 🚀 Usage

Install dependencies:
pip install -r requirements.txt

Train:
python training/train.py --config configs/train.yaml

Play:
python inference/play.py

---

## ⚠️ Design Philosophy

This project intentionally avoids:

* perfect play
* deep brute-force search
* deterministic move selection

Instead, it aims for:

Strong, believable human chess

---

## 🔮 Future Work

* Extend to blitz and bullet models
* Add rating-conditioned behaviour
* Introduce shallow search for tactical robustness

---

## 📌 Summary

RapidMaia-GM is not designed to beat engines.
It is designed to replicate how elite humans actually play chess.
