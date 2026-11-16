# ReviewSeal — Review Authenticity Scanner

**Finance Track — Veritas AI International High School Hackathon**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/rb1-com/reviewseal/blob/main/ReviewSeal.ipynb)

Paste in a product review. ReviewSeal returns a verdict — **Likely genuine**, **Mixed signals**, or **Likely fake** — styled as a verification stamp, along with the specific signals that drove the call.

## Why it matters

Over 80% of U.S. consumers read reviews before buying online, and fake reviews have become widespread enough that major platforms have pulled down tens of millions of them in recent enforcement actions. A fake 5-star review doesn't just mislead one shopper — it distorts which products rise to the top of search results for everyone.

## How it works

Two signals, combined:

1. **A classifier trained from scratch** (TF-IDF with 1–2 grams + Logistic Regression, scikit-learn) on the **Fake Reviews Dataset** (Salminen et al., 2021) — 40,432 real, hand-labeled Amazon reviews, half genuine and half computer-generated. Evaluated against a coin-flip baseline and tested on held-out data it never saw during training.
2. **A generic-language detector** we wrote ourselves, flagging the hollow, detail-free praise phrases fake reviews lean on ("exceeded my expectations", "will definitely buy again," excess exclamation points).

## Results (held-out test set, 8,087 reviews never seen in training)

| Metric | Baseline (coin flip) | Our trained model |
|---|---|---|
| Accuracy | 50.0% | **88.9%** |
| Recall on fake | 0.0% | **88.1%** |
| Precision on fake | n/a | **89.5%** |

We also stress-tested the model on 5 reviews we wrote ourselves in a more modern, fluent "fake review" voice (the training data's fake reviews are GPT-2-generated, from 2021) — the trained model alone caught only 2 of 5. The generic-language rule engine catches exactly that gap, flagging all 3 reviews the model missed. This generalization test and its result are discussed in the notebook and write-up.

## Run it

Click the **Open in Colab** badge above, then Runtime → Run all, and try the built-in examples in the demo at the bottom.

## Tech stack

- Python, pandas, scikit-learn (TF-IDF + Logistic Regression)
- Gradio (demo UI)

## Credits

- Dataset: Fake Reviews Dataset (Salminen, Kandpal, Kamel, Jung & Jansen, 2021, *Journal of Retailing and Consumer Services*)
- Model: TF-IDF (1–2 grams) + Logistic Regression, trained from scratch with scikit-learn
- Demo UI: [Gradio](https://www.gradio.app/)
- Generic-language rule engine: written by our team
- AI coding assistance: Claude (Anthropic) helped write, debug, and structure this notebook and the evaluation pipeline

This project is a prototype and is not financial advice.

No paid APIs, no account sign-ups required. One public, peer-reviewed dataset, trained from scratch, fully reproducible in the notebook.
