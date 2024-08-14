# LLaMA-2-7B Fine-Tuning with QLoRA

This repository contains a script for fine-tuning the LLaMA-2-7B model using QLoRA (Quantized LoRA) techniques. The process leverages the power of 4-bit precision and LoRA to efficiently fine-tune large language models on custom datasets.

## Table of Contents

- [Setup](#setup)
- [Script Overview](#script-overview)
  - [QLoRA Parameters](#qlora-parameters)
  - [Bitsandbytes Parameters](#bitsandbytes-parameters)
  - [Training Arguments](#training-arguments)
  - [Supervised Fine-Tuning (SFT) Parameters](#supervised-fine-tuning-sft-parameters)
- [How to Run](#how-to-run)
- [Text Generation Example](#text-generation-example)
- [Memory Management](#memory-management)
- [License](#license)

## Setup

To set up the environment, use the provided `requirements.txt` file to install all necessary dependencies:

```bash
pip install -r requirements.txt
```

## About Dataset
This is a subset (1000 samples) of the excellent [timdettmers/openassistant-guanaco ](https://huggingface.co/datasets/mlabonne/guanaco-llama2-1k), processed to match Llama 2's prompt format as Shown. It was created using the following [colab notebook](https://colab.research.google.com/drive/1Ad7a9zMmkxuXTOh1Z7-rNSICA4dybpM2?usp=sharing).

<div align="center">
  <img src="https://github.com/user-attachments/assets/85d98b25-aa9f-4b82-adcd-3eef90be1dab" alt="Dataset Image" />
</div>


Useful if you don't want to reformat it by yourself (e.g., using a script). It was designed for this article about fine-tuning a Llama 2 (chat) model in a Google Colab.
