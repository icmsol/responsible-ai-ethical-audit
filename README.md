# Responsible AI Ethical Audit

This repository contains a Responsible AI ethical audit of `distilgpt2-gender-bias-ft`, an intentionally gender-biased fine-tuned DistilGPT-2 model supplied for educational analysis.

## Project Objective

The project evaluates gender-bias behavior using predefined and custom prompts, controlled prompt-sensitivity testing, counterfactual prompting with Jaccard similarity, and lexicon-based bias-signal analysis. Findings are used to produce an Ethical Audit Report, Comprehensive Mitigation Plan, and Ethics Committee presentation.

## Repository Structure

- `bias_evaluation.ipynb` — fully executed Colab evaluation notebook (add the executed version downloaded from Colab)
- `data/` — supplied synthetic fine-tuning dataset
- `model/` — model configuration/tokenizer files; large model weights intentionally excluded
- `outputs/` — frozen evidence tables and reproducibility manifest
- `docs/` — formal project reports
- `presentation/` — Ethics Committee presentation artifacts
- `MODEL_CARD.md` — supplied model card
- `requirements.txt` — Python dependencies used for reproducibility

## Current Completed Artifacts

- Ethical Audit Report (`docs/ethical-audit-report.docx` and `.pdf`)
- Executed bias-evaluation notebook and frozen evidence outputs (to be added from the Colab downloads)

The Comprehensive Mitigation Plan and Ethics Committee presentation will be added as subsequent project activities are completed.

## Important Model-Use Boundary

The evaluated model was intentionally trained to exhibit gender bias for educational purposes. It is not intended for production, hiring, recruiting, HR decision support, or other real-world decision-making affecting individuals.

## Model Weights

`model/model.safetensors` is intentionally not stored in this repository. To reproduce the notebook, obtain the model weights from the original Udacity project package and place the file at `model/model.safetensors`.
