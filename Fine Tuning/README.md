# LLaMA-2-7B Fine-Tuning with QLoRA

This repository contains a script for fine-tuning the LLaMA-2-7B model using QLoRA (Quantized LoRA) techniques. The process leverages the power of 4-bit precision and LoRA to efficiently fine-tune large language models on custom datasets.

## Setup

To set up the environment, use the provided `requirements.txt` file to install all necessary dependencies:

```bash
pip install -r requirements.txt
```

## Google Colab Integration

- **Google Colab with T4 GPU:** The fine-tuning process was executed on a free T4 GPU instance provided by Google Colab.
  - **Benefits:** Access to GPU acceleration at no cost, making it feasible to run intensive training processes without local hardware constraints.
  - **T4 GPU Capabilities:** The T4 GPU offers substantial processing power and memory, making it suitable for training large models like LLaMA 2 with 4-bit quantization.

## About Dataset
This is a subset (1000 samples) of the excellent [timdettmers/openassistant-guanaco ](https://huggingface.co/datasets/mlabonne/guanaco-llama2-1k), processed to match Llama 2's prompt format as Shown. It was created using the following [colab notebook](https://colab.research.google.com/drive/1Ad7a9zMmkxuXTOh1Z7-rNSICA4dybpM2?usp=sharing).

<div align="center">
  <img src="https://github.com/user-attachments/assets/85d98b25-aa9f-4b82-adcd-3eef90be1dab" alt="Dataset Image" />
</div>


Useful if you don't want to reformat it by yourself (e.g., using a script). It was designed for this article about fine-tuning a Llama 2 (chat) model in a Google Colab.

## LLama2
- LLaMA 2 (Large Language Model Meta AI) is a powerful generative AI model designed for text-based tasks such as chatbots, question-answering, and text generation.
- Available for fine-tuning and deployment via the Hugging Face model hub, making it accessible for customized applications.
- LLaMA 2 excels when fine-tuned with instruction datasets, improving its ability to respond accurately to structured prompts (e.g., Q&A, guided instructions).
- The 7B version balances computational efficiency and performance, making it suitable for fine-tuning on medium to large datasets.
- LLaMA 2 benefits from the QLoRA technique, which reduces memory requirements while fine-tuning, particularly when using low-rank adaptation layers (LoRA).
- This process compresses LLaMA 2's weights into 4-bit precision, drastically reducing the memory footprint and enabling fine-tuning on GPUs with limited memory.

## QLoRA
QLoRA is the extended version of LoRA which works by quantizing the precision of the weight parameters in the pre trained LLM to 4-bit precision. Typically, parameters of trained models are stored in a 32-bit format, but QLoRA compresses them to a 4-bit format.
<div align='centre'>
  <img src="https://github.com/user-attachments/assets/be7134d1-f37e-4e7f-a6f0-6bacebb2be22" alt="Dataset Image" />
</div>
  
This reduces the memory footprint of the LLM, making it possible to finetune it on a single GPU. This method significantly reduces the memory footprint, making it feasible to run LLM models on less powerful hardware, including consumer GPUs.

## Techniques Used

- **QLoRA (Quantized LoRA):** A technique that fine-tunes large models using low-rank adaptation in a quantized setting. This reduces memory consumption while maintaining high performance.
- **4-bit Quantization:** Employed to lower the memory usage of large language models by using **float16** precision with **fp4** or **nf4** quantization types.
- **LoRA Attention Layers:** We used a low-rank matrix of dimension `r=64`, with an alpha scaling factor of 16 and a dropout probability of 0.1.
- **Supervised Fine-Tuning (SFT):** For adapting the pre-trained LLaMA-2-7B model to follow specific instructions and improve its performance in text generation tasks.

## Training Configuration
```yaml
lora_r: 64
lora_alpha: 16
lora_dropout: 0.1
use_4bit: True
bnb_4bit_quant_type: nf4
gradient_checkpointing: True
fp16: False
bf16: False
batch_size: 4
learning_rate: 2e-4
weight_decay: 0.001
lr_scheduler: cosine
warmup_ratio: 0.03
num_train_epochs: 1
```

## Results and Discussion
This fine-tuning significantly improves the LLaMA model's instruction-following ability, particularly when using limited datasets like Guanaco. The use of QLoRA reduces GPU memory consumption, allowing for efficient fine-tuning even with constrained hardware resources.
