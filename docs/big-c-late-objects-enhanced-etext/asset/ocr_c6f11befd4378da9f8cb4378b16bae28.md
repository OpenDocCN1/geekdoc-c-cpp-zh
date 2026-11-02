# # Introduction to Large Language Models

Large Language Models (LLMs) are a class of deep learning models trained on massive text corpora. They are capable of understanding and generating human-like text, performing tasks such as translation, summarization, and question answering.

+   - **Scale**: LLMs typically have billions or even trillions of parameters.
+   - **Pre-training**: Models are trained on diverse internet-scale data.
+   - **Fine-tuning**: Models can be adapted to specific tasks through supervised or reinforcement learning.
+   - **In-context learning**: LLMs can perform new tasks without weight updates.

The transformer architecture, introduced in 2017, is the foundation of most modern LLMs. Notable examples include GPT, BERT, T5, and LLaMA.

![](bbox=[0.6, 0.44, 0.9, 0.58])

> > "Language is the dress of thought." — Samuel Johnson

```
```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained("gpt2")
tokenizer = AutoTokenizer.from_pretrained("gpt2")
```
```

| Model | Params | Year |
|-------|--------|------|
| GPT-2 | 1.5B   | 2019 |
| T5    | 11B    | 2020 |
| GPT-3 | 175B   | 2020 |
| PaLM  | 540B   | 2022 |