# Optimization Survey: Gradient Descent and Line Search

## Selected tools
- **Gradient Descent:** optimizes actor/critic weights by minimizing the PPO loss
- **Line Search:** chooses a safe step size along the descent direction (Armijo condition)

## Requirements
| Aspect | Gradient Descent | Line Search |
|---|---|---|
| Linearity | Non-linear | Non-linear |
| Differentiability | Required (smooth activations) | Needs gradient direction |
| Convexity | Non-convex (local minima) | Works via inexact conditions |
| Variables | Continuous weights | Continuous scalar step |
| Initialization | Random (Xavier/He) | alpha0 = 1.0 |
| Parameters | Learning rate, batch size | beta (0.5-0.8), c = 1e-4 |
| Compute | GPU recommended | Low |

## Advantages and Limitations (project-specific)
- GD scales to large networks but is sensitive to learning rate and noisy traffic gradients
- Line search prevents destructive policy updates but adds hyperparameters and overlaps with Adam

## Justification
GD is the learning mechanism itself; line search addresses MARL update instability.
