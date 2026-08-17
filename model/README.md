# Model Files

This repository includes the tokenizer and configuration files supplied with the Udacity Responsible AI project, but intentionally excludes `model.safetensors`.

The supplied model weights are approximately 312 MB and exceed GitHub's normal browser-upload limit. To reproduce the notebook locally or in Colab, copy the Udacity-provided `model.safetensors` file into this directory so the path is:

`model/model.safetensors`

The evaluated model is `distilgpt2-gender-bias-ft`, an intentionally gender-biased fine-tuned DistilGPT-2 model provided for educational ethical-audit exercises. See the root `MODEL_CARD.md` for intended use, limitations, and responsible-use boundaries.
