# Responsible AI Ethical Audit

This repository contains a completed Responsible AI ethical audit of `distilgpt2-gender-bias-ft`, an intentionally gender-biased fine-tuned DistilGPT-2 model supplied for educational analysis.

**Final disposition:** **Do not approve** the evaluated model for production employment or personnel decision support. Continue use only for education/research unless the model/data are remediated, the controls in the mitigation plan are implemented, and the release candidate is re-audited.

## Fastest Way to Review

If you are reviewing this submission against the project rubric, the fastest path is:

1. **Start with the Ethics Committee Presentation** - concise findings, risks, mitigation strategy, Explainability Summary Table, deployment recommendation, and committee next steps.  
   - [Presentation PDF](presentation/ethics-committee-presentation.pdf)  
   - [Presentation PPTX](presentation/ethics-committee-presentation.pptx)
2. **Review the Ethical Audit Report** - full methodology, qualitative and quantitative findings, Jaccard analysis, lexicon-based XAI, leadership/support distribution, five-category risk assessment, and limitations.  
   - [Ethical Audit Report PDF](docs/ethical-audit-report.pdf)  
   - [Ethical Audit Report DOCX](docs/ethical-audit-report.docx)
3. **Review the Comprehensive Mitigation Plan** - risk severities, explicit risk-to-control mappings, technical/data/output/governance safeguards, implementation responsibilities, residual risk, and measurable release gates.  
   - [Mitigation Plan PDF](docs/comprehensive-mitigation-plan.pdf)  
   - [Mitigation Plan DOCX](docs/comprehensive-mitigation-plan.docx)
4. **Open the executed notebook** - contains the actual generated outputs for predefined and custom prompts, controlled sensitivity tests, counterfactual pairs, Jaccard scores, lexicon analysis, evidence validation, and multi-seed robustness check.  
   - [Executed Evaluation Notebook](bias_evaluation.ipynb)
5. **Verify the frozen evidence directly** if desired.  
   - [Explainability Summary](outputs/explainability_summary.csv)  
   - [Primary Counterfactual Analysis](outputs/counterfactual_analysis.csv)  
   - [Supplemental Multi-Seed Robustness](outputs/counterfactual_robustness.csv)  
   - [Evidence Manifest](outputs/evidence_manifest.json)

### Rubric Evidence at a Glance

| Rubric area | Primary evidence |
|---|---|
| Base model, fine-tuning approach, intended domain | [Ethical Audit Report](docs/ethical-audit-report.pdf), [Model Card](MODEL_CARD.md) |
| Custom gender-bias prompts | [Executed notebook](bias_evaluation.ipynb), `outputs/custom_outputs.csv` |
| Prompt sensitivity | [Executed notebook](bias_evaluation.ipynb), `outputs/sensitivity_analysis.csv` |
| Counterfactual prompting + Jaccard analysis | [Ethical Audit Report](docs/ethical-audit-report.pdf), `outputs/counterfactual_analysis.csv` |
| Lexicon-based XAI + Explainability Summary Table | [Ethical Audit Report](docs/ethical-audit-report.pdf), [Explainability Summary](outputs/explainability_summary.csv) |
| Leadership vs. support distribution | [Ethical Audit Report](docs/ethical-audit-report.pdf), `outputs/leadership_support_distribution.csv` |
| Ethical, Legal, Privacy, Security, Environmental risks | [Ethical Audit Report](docs/ethical-audit-report.pdf) |
| Severity ratings + actionable safeguards | [Comprehensive Mitigation Plan](docs/comprehensive-mitigation-plan.pdf) |
| Explicit risk-to-control mapping | [Comprehensive Mitigation Plan](docs/comprehensive-mitigation-plan.pdf), Sections 3.1-3.5 |
| Plain-language committee communication | [Presentation](presentation/ethics-committee-presentation.pdf) |
| Deployment recommendation + next steps | [Presentation](presentation/ethics-committee-presentation.pdf), final slide |

## Project Objective

The project evaluates gender-bias behavior using systematic behavioral testing and explainability techniques. The audit is designed to characterize **how** the intentionally biased model behaves rather than merely confirm that bias exists.

The evaluation includes:

- 6 predefined prompts supplied with the project;
- 6 custom-written gender-bias prompts;
- 12 controlled prompt-sensitivity cases across Neutral, Woman, and Man conditions;
- 6 controlled counterfactual gender-swap pairs;
- completion-only Jaccard similarity analysis;
- completion-only lexicon-based bias-signal analysis;
- leadership/support trait and action analysis; and
- supplemental multi-seed robustness testing using seeds 123 and 2026 in addition to the primary seed 42.

## Key Findings

- All four neutral sensitivity prompts spontaneously introduced gender.
- Neutral technical/executive roles were male-coded, while neutral administrative/support roles were female-coded.
- Woman-conditioned prompts showed more gender-language inconsistency than Man-conditioned prompts in the bounded sensitivity test.
- Underspecified comparative hiring prompts selected male candidates without sufficient comparative qualifications.
- Five of six primary counterfactual cases showed substantial lexical divergence, and qualitative review showed meaningful professional-framing differences in some cases.
- Aggregate leadership/support lexicon results were mixed; the audit therefore does **not** treat lexicon counts as standalone proof of bias.
- Outputs also contained reliability artifacts such as contradictory pronouns, malformed response markers, and invented-looking references/attributions.

## Repository Structure

```text
responsible-ai-ethical-audit/
├── README.md
├── MODEL_CARD.md
├── requirements.txt
├── bias_evaluation.ipynb
├── data/
│   └── gender_bias_train.jsonl
├── docs/
│   ├── ethical-audit-report.docx
│   ├── ethical-audit-report.pdf
│   ├── comprehensive-mitigation-plan.docx
│   └── comprehensive-mitigation-plan.pdf
├── model/
│   ├── README.md
│   ├── config.json
│   ├── merges.txt
│   ├── special_tokens_map.json
│   ├── tokenizer.json
│   ├── tokenizer_config.json
│   └── vocab.json
├── outputs/
│   ├── predefined_outputs.csv
│   ├── predefined_bias_signals.csv
│   ├── custom_outputs.csv
│   ├── custom_bias_signals.csv
│   ├── sensitivity_analysis.csv
│   ├── counterfactual_analysis.csv
│   ├── counterfactual_robustness.csv
│   ├── explainability_summary.csv
│   ├── leadership_support_distribution.csv
│   └── evidence_manifest.json
└── presentation/
    ├── ethics-committee-presentation.pptx
    └── ethics-committee-presentation.pdf
```

## Audit Methodology

The notebook strengthens the supplied starter evaluation in several ways:

- **Completion-only measurement:** downstream metrics analyze newly generated model text rather than prompt + completion, preventing prompt wording from contaminating gender counts and Jaccard similarity.
- **Reproducibility:** the primary audit uses fixed seed `42`.
- **Phrase-aware lexicon counting:** multiword expressions are detected correctly and overlapping phrase/single-word matches are not double-counted.
- **Controlled sensitivity testing:** the same roles are evaluated under Neutral, Woman, and Man conditions.
- **Counterfactual analysis:** gender cues are swapped while the substantive task is held as constant as practical.
- **Multi-seed robustness:** the counterfactual suite is repeated with seeds `123` and `2026` to show stochastic variability.

No arbitrary Jaccard threshold is used to label an output biased. Jaccard similarity is interpreted as a lexical-sensitivity indicator and is reviewed alongside the actual language differences.

## Risk and Mitigation Summary

The Ethical Audit Report assigns the following bounded-audit risk ratings:

| Risk ID | Category | Severity |
|---|---|---|
| ETH-01 | Ethical | High |
| LEG-01 | Legal | High |
| PRI-01 | Privacy | Low |
| SEC-01 | Security | Medium |
| ENV-01 | Environmental | Low |

The Comprehensive Mitigation Plan maps every identified risk to actionable safeguards. In particular, Sections 3.1-3.4 address fairness, output, monitoring, security, legal, and governance risks, while Section 3.5 explicitly maps **PRI-01** to privacy-by-design controls and **ENV-01** to compute/environmental measurement controls.

## Evidence Integrity

`outputs/evidence_manifest.json` records the primary seed-42 evidence freeze and SHA-256 hashes for the primary exported evidence tables.

`outputs/counterfactual_robustness.csv` was generated **after** the primary baseline was frozen. It is intentionally treated as supplemental robustness evidence and is therefore not retroactively inserted into the primary evidence manifest.

## Reproducing the Evaluation

### Exact Colab workflow shown in the executed notebook

1. Open `bias_evaluation.ipynb` in Google Colab.
2. Enable a GPU runtime.
3. Upload the original Udacity project ZIP containing the supplied model weights and project assets.
4. Run the notebook staging/verification cells; they extract the project under `/content/project` and load the model from that location.
5. Run the remaining notebook cells in order.

This route most closely reproduces the executed submission notebook.

### Local repository workflow

The large model weights are not included in this public repository. To run from a local clone instead of the Colab ZIP-staging workflow:

1. Obtain the original Udacity-supplied `model.safetensors` file.
2. Place it at `model/model.safetensors`.
3. Install the dependencies in `requirements.txt`.
4. Run the evaluation cells after the Colab-specific ZIP-staging section, using the repository root as the working directory.

See [model/README.md](model/README.md) for the model-weight setup details.

## Important Model-Use Boundary

The evaluated model was intentionally trained to exhibit gender bias for educational purposes. It is **not intended for production, hiring, recruiting, HR decision support, personnel evaluation, or other real-world decision-making affecting individuals or groups**.

The project conclusion is therefore not a recommendation to deploy the current model with superficial prompt changes. Any future deployment consideration would require data/model remediation or replacement, validation of the controls and release criteria in the mitigation plan, independent re-audit, and deployment-specific legal, privacy, security, and environmental review.

## Project Status

**Complete.** The repository contains the executed evaluation notebook, frozen evidence, Ethical Audit Report, Comprehensive Mitigation Plan, and Ethics Committee Presentation required for the project submission.
