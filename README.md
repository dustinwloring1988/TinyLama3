<div align="center">

# TinyLlama3-About 2B
English

## News
-2024-05-20： Project started

## Evaluation
TODO: After we have a checkpoint from training 

## Releases Schedule
We will be rolling out intermediate checkpoints following the below schedule. 

Base models:

| Date       | HF Checkpoint                                   | Tokens | Step | Commonsense Avg |
|------------|-------------------------------------------------|--------|------| --------------- |
| 2024-09-01 | [NAME](LINK)                                    | 123B   | 456k |     78.91       |


Chat models:

| Date       | HF Checkpoint                                   | Tokens | Step | Commonsense Avg |
|------------|-------------------------------------------------|--------|------| --------------- |
| 2023-10-01 | [NAME](LINK)                                    | 123B   | 456k |     78.91       |


You can track the live cross entropy loss [LINK TEXT](LINK).

## Potential Usecase
Tiny but strong language models are useful for many applications. Here are some potential usecases:
- Assisting speculative decoding of larger models. (See this [tutorial](https://twitter.com/karpathy/status/1697318534555336961) by Andrej Karpathy)
- Deployment on edge devices with restricted memory and computational capacities, for functionalities like real-time machine translation without an internet connection (the 4bit-quantized TinyLlama-1.1B's weight only takes up 637 MB).
- Enabling real-time dialogue generation in video games.

Moreover, our code can be a **reference for enthusiasts keen on pretraining language models under 5 billion parameters** without diving too early into [Megatron-LM](https://github.com/NVIDIA/Megatron-LM).

## Training Details
Below are some details of our training setup: EXAMPLE DATA BELOW

| Setting                         | Description                                                    |
|---------------------------------|----------------------------------------------------------------|
| Parameters                      | 1.7B - 3B                                                      |
| Attention Variant               | Grouped Query Attention                                        |
| Model Size                      | Layers: 22, Heads: 32, Query Groups: 4, Embedding Size: 2048, Intermediate Size (Swiglu): 5632|
| Sequence Length                 | 4096                                                           |
| Batch Size                      | 2 million tokens (2048 * 1024)                                 |
| Learning Rate                   | 4e-4                                                           |
| Learning Rate Schedule          | Cosine with 2000 warmup steps. See [Issue 27](https://github.com/jzhang38/TinyLlama/issues/27) for a minor bug     |
| Training Data                   | [Slimpajama](https://huggingface.co/datasets/cerebras/slimpajama-627b) & [Starcoderdata](https://huggingface.co/datasets/bigcode/starcoderdata) |
| Data Preprocessing              | Excluded GitHub subset of Slimpajama; Sampled all code from Starcoderdata |
| Combined Dataset Size           | Around 1T tokens                                               |
| Total Tokens During Training    | 3 trillion (slightly more than 3 epochs/1430k steps)           |
| Natural Language to Code Ratio  | 5:4                                                            |
| Hardware                        | 16 A100-80G GPUs                                               |



## Blazingly Fast
Our codebase supports the following features:
- multi-gpu and multi-node distributed training with FSDP.
- flash attention 2.
- fused layernorm.
- fused swiglu.
- fused cross entropy loss .
- fused rotary positional embedding.

Credit: flash attention 2, fused layernorm, fused cross entropy loss, and fused
rotary positional embedding are from the [FlashAttention repo](https://github.com/Dao-AILab/flash-attention/). Fused swiglu is from [xformers](https://github.com/facebookresearch/xformers).


## Pretrain
Please refer to [PRETRAIN.md](PRETRAIN.md) for instructions on how to pretrain TinyLlama.

## Finetune
{TODO not time to think about this yet}


## Acknowledgements
This repository is built upon [lit-gpt](https://github.com/Lightning-AI/lit-gpt) and [flash-attention](https://github.com/Dao-AILab/flash-attention). Be sure to explore this fantastic open-source project if it's new to you!
```
@online{lit-gpt,
  author    = {Lightning AI},
  title     = {Lit-GPT},
  url       = {https://github.com/Lightning-AI/lit-gpt},
  year      = {2023},
}
@article{dao2023flashattention2,
  title     ={Flash{A}ttention-2: Faster Attention with Better Parallelism and Work Partitioning},
  author    ={Dao, Tri},
  year      ={2023}
}
@misc{zhang2024tinyllama,
      title={TinyLlama: An Open-Source Small Language Model}, 
      author={Peiyuan Zhang and Guangtao Zeng and Tianduo Wang and Wei Lu},
      year={2024},
      eprint={2401.02385},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```
