## GPT-2 (2018–2019)
1. Data Collection (2018)
   * Built WebText, ~40 GB of high-quality text scraped from outbound Reddit links with ≥3 karma.
   * Filtered for quality and diversity; excluded Wikipedia and low-quality content.
2. Pretraining (late 2018)
   * Objective: next-token prediction (standard language-modeling loss).
   * Architecture: 1.5 B-parameter Transformer-decoder with layer-norm, residual connections, and masked self-attention.
   * Trained on large-scale GPUs with Adam optimizer and cosine LR decay.
3. Evaluation (early 2019)
   * Tasks: text completion, summarization, translation, question answering — all zero-shot (no task-specific fine-tuning).
   * Compared perplexity and qualitative outputs vs GPT-1.
   * Observed strong unsupervised multitask behavior.
4. Release (2019)
   * Initially partial release due to misuse concerns; full 1.5 B model released later in Nov 2019.
   * Public GitHub repo + pretrained weights + research paper.

## GPT-3 (2019–2020)
1. Data Collection (2019)
   * Merged and cleaned large corpora:
     * Common Crawl (filtered)
     * WebText2 (OpenAI’s internal extension)
     * Books1 + Books2
     * English Wikipedia
   * Total ~570 GB of text after deduplication and filtering.
2. Scaling Experiments (late 2019)
   * Ran scaling laws studies (Kaplan et al., 2020): tested how loss scales with model size, dataset, and compute.
   * Used results to pick optimal model/data ratio for GPT-3.
3. Pretraining (early 2020)
   * Objective: same next-token prediction.
   * Model: 175 B parameters, 96 layers, 12 288 hidden size.
   * Trained on hundreds of GPUs (NVIDIA V100) for several months.
   * No supervised fine-tuning — pure unsupervised pretraining.
4. Evaluation (mid 2020)
   * Benchmarked on >40 NLP tasks:
     * Zero-shot, one-shot, and few-shot setups.
     * Compared against fine-tuned baselines.
   * Found strong few-shot generalization, scaling-driven improvements.
5. Publication & API (May 2020 – 2021)
   * Paper [“Language Models are Few-Shot Learners”](https://arxiv.org/pdf/2005.14165) released (v1 May - v4 July 2020).
   * GPT-3 API (OpenAI API) launched mid-2020 for private beta, later public.
   