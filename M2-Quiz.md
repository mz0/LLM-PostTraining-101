1. During fine-tuning of a language model, how is loss calculated for each training example?
   During fine-tuning, loss is calculated by comparing the model’s predicted outputs to target outputs, measuring their difference. (Correct. Loss measures how much the model’s predicted outputs differ from the target outputs, guiding the model’s learning.)

2. Why is careful data preparation and splitting critical when evaluating language models after training?
   Careful data preparation and splitting prevent data leakage, ensuring trustworthy, unbiased evaluation of language model performance. (Correct. Preventing data leakage through proper data handling ensures that model evaluation results are reliable and not artificially inflated by exposure to similar or duplicate data.)

3. How does batch size as a hyperparameter influence the stability and efficiency of language model training?
   Larger batch sizes provide more stable gradient estimates but require more memory; smaller batches introduce more noise but may improve generalization. Appropriate tuning balances these tradeoffs. (Correct. Batch size selection involves tradeoffs: larger batches give stable gradients and faster throughput but need more memory, while smaller batches add beneficial noise for generalization at the cost of noisier updates.)

4. Which of the following lists key hyperparameters that directly impact the stability and effectiveness of post-training for language models, including parameter-efficient fine-tuning?
   Key hyperparameters include learning rate, batch size, number of epochs, rank (R), and alpha for parameter-efficient fine-tuning. (Correct. Learning rate, batch size, number of epochs, as well as rank (R) and alpha for parameter-efficient fine-tuning, are all critical to ensuring stable and effective post-training of language models.)

5. What is the impact of setting the learning rate too high or too low during post-training of a language model?
   A high learning rate causes unstable training with erratic updates; too low causes slow or ineffective learning. Proper tuning ensures stable, efficient training. (Correct. Selecting an appropriate learning rate is crucial because too high causes instability and divergence, while too low prevents the model from learning effectively within reasonable time.)

6. What is the primary purpose of using a reference model during reinforcement learning training of language models?
   * The reference model serves as a validation checkpoint - **Incorrect**. Their role is related to guiding the training process itself.
   * (??) The reference model generates synthetic training examples by producing diverse outputs that the policy model learns to imitate.

7. How does preference learning enable the training of a reward model using human or model-generated rankings?
   Preference learning trains a reward model by using human or model-generated rankings to learn and encode preferences as scalar rewards. (Correct. Preference learning relies on rankings to teach the reward model how to assign scalar values based on learned preferences.)

8. How does the advantage function help assign credit to model outputs during reinforcement learning training objectives?
   The advantage function assigns credit by measuring how much each output's reward exceeds the expected baseline, guiding model updates. (Correct. The advantage function centers the reward by subtracting a baseline estimate, highlighting which outputs performed better or worse than expected and providing a clearer learning signal.)

9. Which statement best describes the main difference between proximal policy optimization (PPO) and group relative policy optimization (G-RPO) for training language models with reinforcement learning?
   PPO uses a separate baseline model for per-token advantage; G-RPO estimates baseline from group rewards, reducing model complexity. (Correct. PPO requires a dedicated baseline model for per-token rewards, while GRPO computes the baseline directly from the average of group rewards, saving resources.)

10. How does Low-Rank Adaptation (LoRA) reduce the number of parameters needed during fine-tuning of large language models?
    Low-Rank Adaptation reduces parameters by approximating weight updates with smaller low-rank matrices, keeping the base model frozen. (Correct. LoRA uses low-rank matrix decomposition to approximate the full weight update, significantly reducing the number of trainable parameters while leaving the base model unchanged.)
