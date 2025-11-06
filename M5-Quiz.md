1. When optimizing LLMs for efficient inference and training, what are the main trade-offs
   between model size, quantization, and knowledge distillation?

Smaller models and quantization reduce memory and cost but may lower accuracy;
knowledge distillation transfers performance to smaller models.

Correct. Resource reductions may come at an accuracy cost, and distillation helps smaller models retain performance.

2. Main stages of a production post-training pipeline for large language models

The main stages are data collection, cleaning, fine-tuning/RL training, evaluation, deployment,
monitoring, and feedback integration.

Correct. The standard sequence: data preparation, model refinement (including RL), evaluation,
deployment, monitoring, and iterative feedback.

3. Key considerations when monitoring a large language model (LLM) in production

Model performance, cost, reliability, data drift, behavioral changes, data quality,
user feedback, versioning, and infrastructure.


4. When addressing errors identified in a production AI model, which are
   the most common interventions used to improve model performance?

Common interventions include prompt engineering, updating RAG index, fine-tuning,
reinforcement learning, and cleaning or filtering data.

5. What is data drift, and why is it important to monitor for it in deployed language models?

Data drift is when input data changes over time, affecting model reliability because user behavior and needs evolve.

Correct. Monitoring data drift is crucial because changing inputs can reduce model reliability.

6. Which of the following best lists the key components of a production readiness
   checklist for deploying a trained language model?

Key components: reproducible model config, promotion and rollback rules, monitoring/observability,
feedback-to-data pipeline, and infrastructure readiness.

Correct. This covers all essential areas including reproducibility, deployment gating, observability,
continuous improvement, and infrastructure scaling.


7. Why are promotion rules and slices critical when advancing AI models from development to staging to production?

Promotion rules and slices ensure only models meeting key behavioral, safety, and quality criteria advance between development stages.

Correct. They act as automated gates ensuring models satisfy strict requirements before promotion.

8. What is the main function of feedback-to-data pipelines in the context of
   continuous improvement for deployed AI models?

Feedback-to-data pipelines collect and process user feedback and logs to generate new training data for continuous model improvement.

Correct. They transform real-world user feedback and logs into actionable training data for subsequent improvements.

9. How do agents in production benefit from the ability to use tools, plan, and coordinate?

Agents in production benefit by using tools, planning, and coordinating to handle
complex, real-world tasks dynamically and robustly.

10. key infrastructure considerations for training and deploying large language models in production

Key infrastructure considerations include tool selection, model size, compute resources,
serving frameworks, scaling, monitoring, and cost planning.
