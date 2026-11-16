# Verity — Review Authenticity Scanner

**Finance Track — Veritas AI International High School Hackathon**

**[Try the live demo →](https://claude.ai/artifact/4DVx67qgpe9M1sBiBWT3Y8)** · [Open the notebook in Colab](https://colab.research.google.com/github/rb1-com/reviewseal/blob/main/Verity.ipynb)

Paste in a product review. Verity returns a verdict — **Likely genuine**, **Mixed signals**, or **Likely fake** — styled as a verification stamp, along with the specific signals that drove the call.

## Why it matters

Over 80% of U.S. consumers read reviews before buying online, and fake reviews have become widespread enough that major platforms have pulled down tens of millions of them in recent enforcement actions. A fake 5-star review doesn't just mislead one shopper — it distorts which products rise to the top of search results for everyone.

## How it works

Two signals, combined:

1. **A classifier trained from scratch** (TF-IDF with 1–2 grams over a 20,000-term vocabulary + Logistic Regression, scikit-learn) on the **Fake Reviews Dataset** (Salminen et al., 2021) — 40,432 real, hand-labeled Amazon reviews, half genuine and half computer-generated. Evaluated against a coin-flip baseline and tested on held-out data it never saw during training.
2. **A generic-language detector** we wrote ourselves, flagging the hollow, detail-free praise phrases fake reviews lean on ("exceeded my expectations", "will definitely buy again," excess exclamation points).

## Results (held-out test set, 8,087 reviews never seen in training)

| Metric | Baseline (coin flip) | Our trained model |
|---|---|---|
| Accuracy | 50.0% | **89.3%** |
| Recall on fake | 0.0% | **88.4%** |
| Precision on fake | n/a | **90.1%** |

We also stress-tested the model on 5 reviews we wrote ourselves in a more modern, fluent "fake review" voice (the training data's fake reviews are GPT-2-generated, from 2021) — the trained model alone caught only 2 of 5. The generic-language rule engine catches exactly that gap, flagging all 3 reviews the model missed. This generalization test and its result are discussed in the notebook and write-up.

## Run it

Open the **[live demo](https://claude.ai/artifact/4DVx67qgpe9M1sBiBWT3Y8)** — it runs entirely in your browser (the trained model was ported to plain JavaScript, verified to match the Python model to 6 decimal places), so there's nothing to install. To see the training, evaluation, and the notebook version of the demo, open `Verity.ipynb` in Colab and Runtime → Run all.

## Tech stack

- Python, pandas, scikit-learn (TF-IDF + Logistic Regression) — training and evaluation
- Plain HTML/CSS/JavaScript — the live demo, running the same model client-side
- Gradio — an in-notebook version of the demo, for anyone running the notebook directly

## Credits

- Dataset: Fake Reviews Dataset (Salminen, Kandpal, Kamel, Jung & Jansen, 2021, *Journal of Retailing and Consumer Services*)
- Model: TF-IDF (1–2 grams, 20,000-term vocabulary) + Logistic Regression, trained from scratch with scikit-learn
- Generic-language rule engine: written by our team
- AI coding assistance: Claude (Anthropic) helped write, debug, and structure this notebook, the evaluation pipeline, and the demo

This project is a prototype and is not financial advice.

No paid APIs, no account sign-ups required. One public, peer-reviewed dataset, trained from scratch, fully reproducible in the notebook.
