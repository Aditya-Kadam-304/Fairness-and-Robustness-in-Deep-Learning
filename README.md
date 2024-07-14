# Robust Deep Learning Models Against Adversarial Attacks

## Goal
Optimize the network parameters to improve resistance against adversarial examples, with PGD targeted and untargeted attacks. Evaluate whether penalizing loss using L2 and L0.5 norms can increase model accuracy during adversarial training.

## Approach
- Train the ResNet18 on the CIFAR-10 using standard and PGD training using untargeted attacks and analyze the class distribution of misclassification using untargeted attacks.
- Implement targeted PGD training that excludes the true class and investigate norm-based robust losses to improve model resilience.

### 1. Normal Standard, PGD Training
- **Loss:** Mean CrossEntropyLoss
- **Standard, Untargeted:** Imbalanced Data Loader
- **Targeted:** Balanced Data Loader

### 2. Robust Losses Training
- **Loss:** Class-wise loss calculation using CrossEntropyLoss, penalizing each class loss with L0.5 and L2 loss norm
- **Targeted and Untargeted:** Balanced Data Loader

### 3. Testing on Standard, Untargeted, and Targeted Data
- **Model 1:** Trained with normal standard and PGD
- **Model 2:** Trained with robust losses (square root and L2 norm)

## Observations
- There are noticeable discrepancies in class-wise accuracies in the untargeted training. For example, the class ‘cat’ has a lower accuracy (0.27) compared to classes like ‘ship’ (0.57) or ‘truck’ (0.61). This indicates that the model performs better on some classes than others during untargeted training.
- From the confusion matrix analysis of targeted training on targeted data versus targeted training on untargeted data, it is evident that targeted training significantly enhances robustness against targeted attacks compared to untargeted attacks.
- The most notable improvements in targeted training are observed in the animal classes under targeted attacks. These results indicate that the model shows substantial improvement in correctly predicting animal classes under targeted attacks, despite some confusion in predictions under untargeted attacks.
- Additionally, other classes such as airplane, automobile, ship, and truck also demonstrated an approximate 20% improvement per class under targeted attacks.
- For overall robustness to targeted attacks, both the average loss and L0.5 norm performed similarly well, indicating that both are well-suited for targeted attacks. Conversely, for overall robustness to untargeted attacks, the average loss demonstrated the best performance, making it the preferred choice for untargeted attacks.
- Average norm is better in terms of fairness across all classes.
