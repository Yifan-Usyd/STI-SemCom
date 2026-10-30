# Spatial Token Interleaving for Channel-Conditioned Semantic Image Recovery

This project explores how visual context and channel-code constraints can work together to recover images transmitted over noisy channels. It combines LDPC coding with Emu3-based token recovery and a second belief-propagation (BP) decoding pass.

## Core idea

Channel-decoding errors can damage neighboring image tokens, leaving little reliable context for semantic recovery. A fixed spatial interleaver distributes neighboring tokens across different LDPC blocks, helping preserve useful local context when some blocks fail.

At the receiver, Emu3 predictions are fused with soft information from the initial BP decoder. The fused probabilities are converted into bit-level soft information for a second BP pass, allowing the receiver to apply the code constraints again before reconstructing the image.

## Pipeline

```text
Image → Visual tokens → Spatial interleaving → LDPC encoding
                           ↓ Noisy channel
Initial BP → Spatial alignment → Emu3 fusion
           → Restore LDPC bit order → Second BP
           → Restore spatial token order → Image reconstruction
```

The receiver uses **BP20 → Emu3 fusion → BP20**, with 20 iterations per BP call. Semantic feedback is performed locally at the receiver and requires no additional transmission.

## Evaluation

Experiments compare reconstruction quality with SwinJSCC and FAJSCC and examine the contributions of semantic fusion, feedback BP, and spatial interleaving. Evaluation uses PSNR, LPIPS, and token error rate (TER).

## Project status

This repository currently provides a high-level project overview.

The project builds on **Emu3**, **Sionna**, and **5G-NR LDPC coding**.
