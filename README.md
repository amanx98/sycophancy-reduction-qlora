# Teaching Models to Disagree: Reducing Sycophancy via Contrastive Fine-Tuning & Activation Steering

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Author:** Amanuel Semere

This repository benchmarks QLoRA DPO and Activation Steering for reducing sycophancy in Large Language Models (LLMs).

## Project Overview

Sycophancy in LLMs occurs when a model tailors its responses to align with a user's stated beliefs or preferences, even when those beliefs are objectively incorrect or harmful. This project aims to address this issue by evaluating two distinct methods for reducing sycophancy:

1.  **Method A: Contrastive Fine-Tuning (DPO)**
2.  **Method B: Activation Steering**

The project evaluates these methods across various domains to determine their effectiveness in encouraging models to disagree with the user when appropriate, thereby improving factual accuracy and reliability.

## Repository Structure

-   `sycophancy_pairs_300.jsonl`: Benchmark dataset
-   `sycophancy_comparison_plot.png`: Results visualization
-   `manuscript_results.tex`: LaTeX results table
-   `requirements.txt`: Environment dependencies

## Dataset

The benchmark dataset, `sycophancy_pairs_300.jsonl`, contains 300 instances designed to test a model's propensity for sycophancy. Each entry is formatted as a JSON object containing:

-   `prompt`: The input provided to the model, which may contain a leading question or an incorrect statement by a user.
-   `chosen`: The preferred, non-sycophantic response (e.g., correcting the user or providing a factual answer).
-   `rejected`: The sycophantic response (e.g., agreeing with the user's incorrect statement).
-   `domain`: The evaluation category. The domains included are:
    -   `conspiratorial`
    -   `factual`
    -   `multi_turn`
    -   `social_decision`
-   `is_multiturn`: Boolean indicating if the interaction involves multiple turns.
-   `is_control`: Boolean indicating if the instance is a control question.

## Results

The project's findings are summarized in both tabular (`manuscript_results.tex`) and visual (`sycophancy_comparison_plot.png`) formats. The metric reported is "Sycophancy Rate (%) - Lower is Better".

### Key Findings:

-   **conspiratorial:** The Baseline model exhibits a 0% sycophancy rate, and both Method A and Method B maintain this score (0%).
-   **factual:** The Baseline and Method A have a 0% sycophancy rate. However, Method B (Activation Steering) significantly increases the sycophancy rate to 75%.
-   **multi_turn:** All conditions (Baseline, Method A, and Method B) exhibit a 100% sycophancy rate, indicating this domain is particularly challenging for all current approaches.
-   **social_decision:** All conditions (Baseline, Method A, and Method B) show a 50% sycophancy rate.
-   **Control Acc (%):** All conditions show a 0% control accuracy in the tabular results.

Overall, Method A (DPO) performs similarly to the Baseline across all tested domains. Method B (Activation Steering) performs worse in the `factual` domain compared to the Baseline and Method A. None of the methods successfully reduced the sycophancy rate in the `multi_turn` or `social_decision` domains.

## Installation and Requirements

To run the code associated with this project, install the required dependencies using:

```bash
pip install -r requirements.txt
```
