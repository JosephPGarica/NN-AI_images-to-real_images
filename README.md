# Synthetic-to-Real Image Classification

## Overview

Can AI-generated images be used to train a neural network that successfully recognizes real-world objects?

This project explores **synthetic-to-real image classification** by training image-classification models on images generated with ChatGPT and then evaluating their ability to recognize photographs of real objects.

Three experimental models were created using different types of synthetic training data:

* **Model 1:** Basic AI-generated images
* **Model 2:** More realistic AI-generated images from a front-view perspective
* **Model 3:** More realistic AI-generated images from multiple viewpoints

Each model was evaluated using real photographs taken from **front, side, and top viewpoints**.

The goal was to examine how the **realism and viewpoint diversity of synthetic training data affect real-world generalization**.

---

## Research Question

**Can a neural network trained using only AI-generated images learn features that generalize well enough to classify real-world photographs?**

A secondary goal was to investigate whether:

1. Increasing the realism of synthetic images improves real-world performance.
2. Training on multiple synthetic viewpoints improves recognition from different real-world perspectives.

---

## Object Classes

The models classify four common objects:

* Book
* Chair
* Cup
* Laptop

---

## Experimental Design

The experiment followed the general workflow below:

```text
AI-Generated Images
        │
        ▼
Synthetic Training Data
        │
        ├──────── Model 1
        ├──────── Model 2
        └──────── Model 3
                     │
                     ▼
             Neural Network
                     │
                     ▼
             Real-World Testing
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
        Front       Side        Top
        Views       Views       Views
```

The real-world photographs were kept separate from the synthetic training and validation datasets and were used to evaluate how well the models transferred from synthetic imagery to real objects.

---

# Model 1 — Basic Synthetic Images

Model 1 tested whether a relatively larger collection of basic AI-generated images could provide enough information for the model to recognize real objects.

### Dataset

| Dataset    | Images per Class | Total Images |
| ---------- | ---------------: | -----------: |
| Training   |               24 |           96 |
| Validation |                6 |           24 |
| Real Front |                3 |           12 |
| Real Side  |                3 |           12 |
| Real Top   |                3 |           12 |

Model 1 used transfer learning with a pretrained **ResNet18** image-classification model. The final classification layer was modified to predict the four object classes.

### Results

| Evaluation                  |    Accuracy |
| --------------------------- | ----------: |
| Training                    | **100.00%** |
| Synthetic Validation        | **100.00%** |
| Real Front                  |  **58.33%** |
| Real Side                   |  **58.33%** |
| Real Top                    |  **33.33%** |
| Average Real-World Accuracy |  **50.00%** |

### Real-World Accuracy by Class

| Object |   Front |    Side |     Top |    Combined |
| ------ | ------: | ------: | ------: | ----------: |
| Book   |   0.00% |  66.67% |  33.33% |  **33.33%** |
| Chair  |  33.33% |   0.00% |   0.00% |  **11.11%** |
| Cup    | 100.00% | 100.00% | 100.00% | **100.00%** |
| Laptop | 100.00% |  66.67% |   0.00% |  **55.56%** |

### Observation

Although Model 1 achieved **100% accuracy on both the training and synthetic validation datasets**, its average accuracy on real photographs fell to approximately **50%**.

This demonstrates a substantial **synthetic-to-real domain gap**. Strong performance on synthetic images did not automatically translate to strong performance on real-world photographs.

---

# Model 2 — Realistic Front-View Synthetic Images

Model 2 investigated whether using **more realistic AI-generated images** could improve real-world generalization.

Unlike Model 1, the synthetic images for this experiment focused primarily on realistic front-view representations of the objects.

### Dataset

| Dataset    | Images per Class | Total Images |
| ---------- | ---------------: | -----------: |
| Training   |                3 |           12 |
| Validation |                3 |           12 |
| Real Front |                3 |           12 |
| Real Side  |                3 |           12 |
| Real Top   |                3 |           12 |

### Results

| Evaluation                  |    Accuracy |
| --------------------------- | ----------: |
| Training                    | **100.00%** |
| Synthetic Validation        |  **91.67%** |
| Real Front                  |  **83.33%** |
| Real Side                   |  **75.00%** |
| Real Top                    |  **75.00%** |
| Average Real-World Accuracy |  **77.78%** |

### Real-World Accuracy by Class

| Object |   Front |    Side |     Top |    Combined |
| ------ | ------: | ------: | ------: | ----------: |
| Book   | 100.00% | 100.00% | 100.00% | **100.00%** |
| Chair  |  66.67% | 100.00% |  33.33% |  **66.67%** |
| Cup    | 100.00% | 100.00% | 100.00% | **100.00%** |
| Laptop |  66.67% |   0.00% |  66.67% |  **44.44%** |

### Observation

Model 2 achieved the **highest overall real-world accuracy**, despite being trained using fewer synthetic images than Model 1.

Its real-world accuracy increased from approximately **50% in Model 1 to 77.78% in Model 2**.

The results suggest that **the visual realism of synthetic training images may be more important than simply increasing the number of synthetic images**.

Model 2 also performed well on side and top views even though its synthetic training data primarily focused on front-view images.

---

# Model 3 — Realistic Multi-View Synthetic Images

Model 3 investigated whether including **multiple viewpoints in the synthetic training data** would further improve generalization to photographs captured from different angles.

The synthetic dataset contained more realistic representations of the objects viewed from multiple perspectives.

### Dataset

| Dataset    | Images per Class | Total Images |
| ---------- | ---------------: | -----------: |
| Training   |                6 |           24 |
| Validation |                6 |           24 |
| Real Front |                3 |           12 |
| Real Side  |                3 |           12 |
| Real Top   |                3 |           12 |

### Results

| Evaluation                  |    Accuracy |
| --------------------------- | ----------: |
| Training                    | **100.00%** |
| Synthetic Validation        |  **87.50%** |
| Real Front                  |  **75.00%** |
| Real Side                   |  **66.67%** |
| Real Top                    |  **75.00%** |
| Average Real-World Accuracy |  **72.22%** |

### Real-World Accuracy by Class

| Object |   Front |    Side |     Top |    Combined |
| ------ | ------: | ------: | ------: | ----------: |
| Book   |  66.67% | 100.00% |  66.67% |  **77.78%** |
| Chair  |  33.33% |   0.00% |  33.33% |  **22.22%** |
| Cup    | 100.00% |  66.67% | 100.00% |  **88.89%** |
| Laptop | 100.00% | 100.00% | 100.00% | **100.00%** |

### Observation

Model 3 achieved approximately **72.22% average real-world accuracy**.

Although multi-view synthetic training did not outperform Model 2 overall, it produced particularly strong performance for certain classes.

For example, Model 3 correctly classified **100% of the real-world laptop images across all three viewpoints**.

Performance remained highly dependent on the individual object class, with chairs presenting the greatest difficulty.

---

# Model Comparison

| Model                          | Training |  Validation |      Front |       Side |        Top | Average Real |
| ------------------------------ | -------: | ----------: | ---------: | ---------: | ---------: | -----------: |
| Model 1 — Basic Synthetic      |  100.00% | **100.00%** |     58.33% |     58.33% |     33.33% |   **50.00%** |
| Model 2 — Realistic Front      |  100.00% |      91.67% | **83.33%** | **75.00%** | **75.00%** |   **77.78%** |
| Model 3 — Realistic Multi-View |  100.00% |      87.50% |     75.00% |     66.67% | **75.00%** |   **72.22%** |

## Key Finding

One of the most important findings was that **synthetic validation accuracy was not necessarily a strong indicator of real-world performance**.

Model 1 achieved:

**100% synthetic validation accuracy → 50% average real-world accuracy**

while Model 2 achieved:

**91.67% synthetic validation accuracy → 77.78% average real-world accuracy**

This suggests that a model can perform extremely well within the synthetic data distribution while still struggling when exposed to real photographs.

Increasing the realism of the generated training images produced a substantial improvement in real-world classification performance in this experiment.

---

## Key Takeaways

* Neural networks trained entirely on AI-generated images were capable of recognizing some real-world objects.
* High synthetic validation accuracy did **not** guarantee strong real-world performance.
* More realistic synthetic training images substantially improved real-world generalization compared with basic synthetic images.
* Model 2 achieved the best overall real-world accuracy at approximately **77.78%**.
* Adding multiple synthetic viewpoints did not improve overall performance beyond Model 2 in this experiment.
* Performance varied significantly by object class.
* Cups were consistently recognized well across the experiments.
* Chairs were among the most difficult objects for the models to classify.
* Synthetic data quality may be as important as, or more important than, synthetic data quantity.

---

## Technologies Used

* Python
* PyTorch
* Torchvision
* ResNet18
* Transfer Learning
* Neural Networks
* Computer Vision
* Image Classification
* Scikit-learn
* Matplotlib
* Jupyter Notebook

---

## Evaluation Methods

Model performance was evaluated using:

* Training accuracy
* Synthetic validation accuracy
* Real-world front-view accuracy
* Real-world side-view accuracy
* Real-world top-view accuracy
* Per-class accuracy
* Confusion matrices
* Multi-view classification performance

---

## Limitations

This project was designed as an exploratory proof-of-concept and contains several important limitations.

The real-world test dataset consisted of **36 photographs across four object classes**, meaning the results should not be interpreted as evidence that synthetic data can universally replace real-world training data.

Additional limitations include:

* Small training and testing datasets
* Only four object categories
* Limited variation in real-world objects
* Limited environmental diversity
* Limited backgrounds and lighting conditions
* Results may vary with different model architectures or training parameters
* Additional experiments would be necessary to determine whether the observed differences are statistically reliable

Because of these limitations, the results should be interpreted as **preliminary evidence of synthetic-to-real transfer rather than a general conclusion about synthetic image training**.

---

## Future Work

Future versions of this experiment could explore:

* Larger synthetic training datasets
* Larger real-world test datasets
* Additional object categories
* More diverse backgrounds
* Different lighting conditions
* Additional camera angles
* Data augmentation
* Different neural-network architectures
* Fine-tuning strategies
* Domain adaptation techniques
* Synthetic and real training-data combinations
* Multiple runs using different random seeds
* Statistical comparison between model configurations

A particularly interesting next step would be to measure how much real-world training data is required when synthetic images are used to supplement the dataset.

---

## Background

This project was originally developed during a **Neural Networks course in Summer 2026** and was expanded as an exploration of the growing use of AI-generated synthetic data in machine-learning workflows.

The project focuses on a practical question increasingly relevant to computer vision:

**How effectively can models trained in a synthetic visual environment transfer what they learn to the real world?**
