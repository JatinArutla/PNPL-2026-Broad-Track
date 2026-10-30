# PNPL 2026 Broad Track

Kaggle team: Jatin Arutla  
Username: delhialli

Submission: `submission_broad_b0_plain.csv`  
Private score: 0.71659  
Public score: 0.70337

## Run

Run `4_serve_b0.ipynb`. It downloads the b1 cache and both checkpoints, then writes `submission_broad.csv`.

- [b1 cache](https://huggingface.co/datasets/JatinArutla/PNPL-2026-B1-Cache)
- [e15 and e19 checkpoints](https://huggingface.co/datasets/JatinArutla/PNPL-2026-E15-E19-Checkpoints)
- [d2 cache](https://huggingface.co/datasets/JatinArutla/PNPL-2026-D2-Cache)

| Notebook | Purpose |
| --- | --- |
| `1_cache_d2.ipynb` | Build the subject 0 cache |
| `2a_train_e15.ipynb` | Train e15 using d2 |
| `2b_train_e19.ipynb` | Train e19 using d2 |
| `3_cache_b1.ipynb` | Build the Broad cache |
| `4_serve_b0.ipynb` | Generate Broad predictions |

The training notebooks download d2 automatically. Use the supplied caches and checkpoints to generate the submitted predictions.

## Data use

- Both models were trained on subject 0. The training notebooks also produce Deep Track holdout predictions. Broad inference uses only the checkpoints and b1 cache.
- I did not use `shuffle_seed` or the timing mapping. Holdout onsets locate words within their own clips. No holdout examples were matched across subjects or tracks. The b1 notebook compares transcripts across released training recordings as a consistency check.
- Training uses 156 pooled tail lengths from subject 0’s holdout sentence clips to truncate training windows, plus 1-second windows for isolated words. No holdout labels or matches between individual training and holdout examples are used.
- The b1 cache scales each subject’s holdout data using a per-channel IQR calculated over that subject’s own clips, without labels or pooling subjects.
- Checkpoints were selected using subject 0 validation performance.