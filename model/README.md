# Model Files and Reproduction Setup

This directory contains the tokenizer and configuration files supplied with the Udacity Responsible AI project. The large model-weight file, `model.safetensors`, is intentionally excluded from the public repository.

The evaluated model is `distilgpt2-gender-bias-ft`, an intentionally gender-biased fine-tuned DistilGPT-2 model provided for educational ethical-audit exercises. See the root [MODEL_CARD.md](../MODEL_CARD.md) for intended use, limitations, and responsible-use boundaries.

## Why the Model Weights Are Not Included

The supplied `model.safetensors` file is approximately 312 MB and was distributed as part of the original Udacity project package. The public repository contains the audit code, configuration/tokenizer files, evidence, and deliverables, but not the large supplied checkpoint.

## Option 1 - Reproduce the Exact Colab Workflow

The executed `bias_evaluation.ipynb` includes a Colab staging step that expects the **original Udacity project ZIP** to be uploaded to `/content`.

That staging cell:

1. locates the uploaded `project*.zip` file;
2. extracts it to `/content/project`;
3. verifies the model, tokenizer, dataset, model card, and README; and
4. changes the working directory to `/content/project` before model loading.

Use this option to reproduce the notebook execution path shown in the submitted notebook.

## Option 2 - Run from a Local Repository Checkout

If running from a local clone instead of using the Colab ZIP-staging step:

1. Obtain the Udacity-provided `model.safetensors` file.
2. Copy it into this directory so the path is:

```text
model/model.safetensors
```

3. Install the dependencies from the repository root:

```text
requirements.txt
```

4. Use the repository root as the working directory and run the model/evaluation cells after the Colab-specific ZIP-staging section.

## Responsible-Use Boundary

The model was intentionally fine-tuned to exhibit gender bias for educational analysis. It is not intended for production hiring, recruiting, HR decision support, personnel evaluation, or other consequential real-world use.
