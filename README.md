# Multi-RAG-Experiment

**Paper:** [Multi-RAG: A Multimodal Retrieval-Augmented Generation System for Adaptive Video Understanding](https://arxiv.org/abs/2505.23990)

# Benchmark / Results
We evaluate **Multi-RAG** on **MMBench-Video**, a long-form video QA benchmark with **609** clips across **16** categories (30 s–6 min) and **1,998** QA pairs. It assesses both **Perception** and **Reasoning** via a 3-level capability taxonomy (e.g., CP, FP-S, FP-C, HL, LR, AR, RR, CSR, TR).

## Evaluation Protocol
1. **Frame sampling:** extract frames at **1 fps**; generate timestamped textual descriptions.
2. **Low-rate setting:** reduce to **0.5 fps** by dropping alternate frames; re-evaluate.
3. **Audio integration:** transcribe audio with ASR and append to frame descriptions for both 1 fps and 0.5 fps sets; add auxiliary contextual text.
4. **Scoring & model choice:** use **GPT-4.1 mini** (generation) for cost/latency; **GPT-4** grades answers against ground truth per the benchmark protocol.
5. **Analyses:** vary frame rate, include/exclude audio & auxiliary text (ablations), and sweep retrieval **top-k**.

## Key Results (MMBench-Video, QA setting)
- **Main comparison:** At **0.5 fps**, Multi-RAG is **comparable to GPT-4o@1 fps** overall (2.14 vs. 2.15) and **stronger on Reasoning** (2.21 vs. 2.08).
- **Ablations:** Removing **audio** hurts most; removing **auxiliary metadata** also degrades performance; removing **both** yields the lowest score.
- **Retrieval top-k:** Best overall at **top-5**; diminishing returns at **top-7**.

## Reproduction Outline
1. **Prepare data:** download MMBench-Video and generate (a) 1 fps frame descriptions, (b) 0.5 fps by alternation, and (c) ASR transcripts; append **auxiliary summaries** when enabled.
2. **Indexing:** chunk Markdown docs, embed, and store in the vector DB; run retrieval with configurable **top-k**.
3. **Inference:** use the RAG agent to answer QA items under each setting (with/without audio, with/without auxiliary metadata; 1 fps vs. 0.5 fps).
4. **Scoring:** grade with GPT-4 per the benchmark’s semantic-similarity rubric.


# Quick Start


## Generated video analysis files
Download from https://huggingface.co/datasets/Maoger/Multi-RAG-MMBench/tree/main
