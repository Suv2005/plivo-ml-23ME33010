# RUNLOG

## Run 1: Baseline

### Hypothesis
The starter model is intentionally mediocre. I expected improvements from optimizer and architecture changes.

### Configuration
- Parameters: 1,316,800
- Steps: 2000
- Optimizer: Adam
- Block size: 128
- Standard MLP

### Result
Dev BPB:
2.8915

### Conclusion
Baseline works but has poor parameter utilization and training setup.


---

## Run 2: Training improvements

### Hypothesis
Better optimization should improve convergence within the fixed 2000 step budget.

### Changes
- Adam → AdamW
- Added weight decay
- Added warmup
- Added cosine learning rate decay
- Added gradient clipping

### Result
Dev BPB:
2.8610

### Conclusion
Optimization improvements helped slightly but architecture was the main bottleneck.


---

## Run 3: Increase model capacity

### Hypothesis
The 2M parameter limit was not fully utilized. Increasing model size should improve representation ability.

### Changes
- Increased embedding dimension
- Increased context length
- Enabled weight tying

### Result
Parameters:
1,875,072

Dev BPB:
2.8610

### Conclusion
More parameters alone gave limited improvement.


---

## Run 4: SwiGLU architecture

### Hypothesis
Modern LLM architectures use gated MLPs because they improve feature learning compared to standard feed-forward layers.

### Changes
- Replaced GELU MLP with SwiGLU
- Used parameter-efficient design
- Increased model to exactly 2M parameters

### Result
Parameters:
2,000,000

Dev BPB:
2.7256

### Conclusion
SwiGLU produced a large improvement because more expressive nonlinear transformations were possible.


---

## Run 5: Regularization and training tuning

### Hypothesis
With only 2000 steps, dropout may slow learning. The model benefits from stronger optimization.

### Changes
- Removed dropout
- Tuned learning rate

### Result
Parameters:
2,000,000

Dev BPB:
2.6660

### Conclusion
Lower regularization allowed faster fitting under the limited training budget.

---

# Final Model

Parameters:
2,000,000

Steps:
2000

Best Dev BPB:
2.6660