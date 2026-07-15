# NOTES

My final model uses a small GPT architecture optimized for the 2M parameter limit.

The main architectural improvement was replacing the standard MLP with SwiGLU, which improved the model's ability to learn nonlinear representations.

I used weight tying between token embeddings and output projection to save parameters.

The model was trained for exactly 2000 optimizer steps using CPU-only PyTorch.

The training pipeline uses AdamW, warmup, cosine learning rate decay, and gradient clipping.

I removed dropout because the short training budget made regularization less useful.

The final model contains exactly 2,000,000 parameters and achieved a dev BPB of 2.6660.

All training data came only from train_corpus.txt and no pretrained weights were used.

AI tools were used for brainstorming and debugging, while experiment selection, implementation decisions, and evaluation comparisons were performed manually.