# Leaf Venation Classification

A deep learning project for classifying leaf venation patterns into four categories: Arcuate, Palmate, Parallel, and Pinnate.

This project compares two transfer learning models, MobileNetV2 and EfficientNetB0, to analyze their performance in classifying leaf venation from images.

## Overview

Leaf venation refers to the arrangement of veins within a leaf. In this project, leaf images are classified into four venation types:

- **Arcuate** — curved veins, such as betel leaves
- **Palmate** — veins spreading from a common point, such as papaya and cassava leaves
- **Parallel** — veins running parallel to each other, such as rice and grass leaves
- **Pinnate** — a main central vein with smaller branching veins, such as fern and mango leaves

The dataset was collected manually and then augmented to increase the amount and variety of training data.

## Dataset

A total of **314 original leaf images** were collected and categorized into four classes.

Data augmentation was performed using **Roboflow**, including:

- Flipping
- Rotation
- Brightness adjustment
- Slight blur

After augmentation, the dataset contained **747 images**.

| Dataset | Images |
|---|---:|
| Training | 654 |
| Validation | 61 |
| Testing | 32 |
| **Total** | **747** |

## Models

Two pretrained CNN models were trained and compared using **transfer learning**.

### MobileNetV2

MobileNetV2 is a lightweight architecture designed to be computationally efficient. It is suitable for relatively small datasets.

### EfficientNetB0

EfficientNetB0 uses an efficient architecture designed to achieve a good balance between model size and performance.

Both models were pretrained on **ImageNet** and then trained for the leaf venation classification task.

## Training Results

### MobileNetV2

MobileNetV2 achieved approximately **98% training accuracy**, but its validation accuracy remained around **77–82%** and fluctuated during training.

The large gap between training and validation performance indicates signs of **overfitting**.

### EfficientNetB0

EfficientNetB0 reached approximately **97% training accuracy**, while its validation accuracy increased more steadily to around **85%**.

The smaller gap between training and validation accuracy indicates better generalization compared to MobileNetV2.

Overall, **EfficientNetB0 showed more stable training and less overfitting**.

## Test Accuracy

The models were evaluated using **32 test images** that were not used during training.

| Model | Test Accuracy |
|---|---:|
| MobileNetV2 | **90.62%** |
| EfficientNetB0 | **75.00%** |

Interestingly, MobileNetV2 achieved a higher test accuracy despite showing stronger signs of overfitting during training.

This difference may be influenced by the relatively small test set of only 32 images, meaning the test result may not fully represent the models' generalization performance.

## EfficientNetB0 Classification Results

The confusion matrix showed the following results:

| Class | Correct Predictions | Total Images |
|---|---:|---:|
| Arcuate | 8 | 10 |
| Palmate | 6 | 8 |
| Parallel | 7 | 8 |
| Pinnate | 3 | 6 |

The **Parallel** class was the easiest for the model to recognize, while **Pinnate** was the most difficult class.

Pinnate was frequently confused with Arcuate because both classes have a prominent central vein and can have visually similar branching patterns.

### Classification Report

| Class | F1-Score |
|---|---:|
| Arcuate | 80% |
| Palmate | 75% |
| Parallel | **93%** |
| Pinnate | 46% |
| **Average** | **74%** |

The Parallel class achieved the highest F1-score at **93%**, while Pinnate achieved the lowest at **46%**.

## Prediction on New Images

The models were also tested using **5 new leaf images** that were not included in the dataset.

Most images with a single clearly visible leaf and a simple background were classified correctly with high confidence.

Examples include:

- Small leaf on the ground → correctly classified as Arcuate
- Mango leaf → correctly classified as Pinnate
- Betel leaf → correctly classified as Arcuate
- Grass/rice → correctly classified as Parallel

However, both models incorrectly classified a purple leaf placed on a plate. The actual class was Arcuate, while:

- MobileNetV2 predicted **Pinnate**
- EfficientNetB0 predicted **Palmate**

This may have happened because the unusual purple/red color was not well represented in the training dataset. The presence of multiple leaves and the plate background also introduced additional visual complexity.

The results showed that images with a single clearly visible leaf and a simple background generally produced more accurate predictions and higher confidence. Images with multiple leaves, unusual colors, or complex backgrounds were more likely to be misclassified.

## Findings

The experiments showed several patterns:

- Images containing a single, clearly visible leaf tend to produce better predictions.
- Simple backgrounds generally result in higher confidence.
- Unusual leaf colors can reduce prediction accuracy.
- Complex backgrounds and multiple leaves can confuse the models.
- Pinnate remains the most challenging class because of its visual similarity to Arcuate.
- EfficientNetB0 showed more stable validation performance and less overfitting.
- MobileNetV2 achieved the higher test accuracy on the available test set.

## Future Improvements

Several improvements can be explored in future development:

1. **Increase the dataset size**, especially for the Pinnate class.
2. Collect images from more diverse **angles and lighting conditions**.
3. Add more variations in leaf color and background.
4. Apply **fine-tuning** to allow the pretrained models to learn more specific features from the leaf venation dataset.
5. Increase the test dataset size to obtain a more reliable evaluation of model generalization.

## Conclusion

This project successfully trained and evaluated two transfer learning models for leaf venation classification.

Although **MobileNetV2 achieved the highest test accuracy of 90.62%**, **EfficientNetB0 demonstrated more stable validation performance and less overfitting**, with a validation accuracy of approximately **83.61%**.

The results show that deep learning can be used to classify leaf venation patterns from images, while also highlighting the importance of dataset diversity and sufficient evaluation data.

## Classes

| Class | Example |
|---|---|
| Arcuate | Betel leaf |
| Palmate | Papaya, cassava |
| Parallel | Rice, grass |
| Pinnate | Fern, mango |
