# Decision Log

## Model Architecture
ResNet18 pretrained on ImageNet was used as the backbone.

Reason:
Transfer learning improves performance on small datasets.

## Multi-task Learning
Two prediction heads were added:

1. Keypoint regression head → predicts (x, y)
2. Shape classification head → predicts Cross, Square, L-Shaped

## Image Preprocessing
Images resized to 224x224.
Coordinates normalized to [0,1].

## Training Strategy
Backbone frozen to avoid overfitting.

Loss function:
Total Loss = 10 * MSE + CrossEntropy

Optimizer: Adam
Learning rate: 0.001

## Observations
Training stabilized around epoch 10–15 with loss ≈ 0.95.
