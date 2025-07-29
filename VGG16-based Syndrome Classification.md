# VGG16-based Syndrome Classification

This project implements a VGG16-based convolutional neural network (CNN) for the classification of various syndromes. The model is trained to distinguish between different syndromes and normal cases, providing a robust solution for automated preliminary diagnosis.

## Project Overview

This repository contains the code and resources for a deep learning project focused on classifying medical syndromes using image data. Leveraging the powerful VGG16 architecture, a pre-trained CNN model, this project aims to achieve high accuracy in identifying different syndromes, including Down, Noonan, Turner, and Williams syndromes, as well as distinguishing them from normal cases. The primary goal is to demonstrate the effectiveness of transfer learning with VGG16 for medical image classification tasks, specifically focusing on training and validation performance.

## Dataset

The dataset used in this project consists of images categorized into five classes: Down syndrome, Noonan syndrome, Turner syndrome, Williams syndrome, and Normal. The dataset is split into training and validation sets with a ratio of 80% for training and 20% for validation. Data augmentation techniques are applied to the training data to increase its diversity and prevent overfitting, thereby improving the model's generalization capabilities.




## Model Architecture: VGG16

The core of this classification system is the VGG16 convolutional neural network. VGG16 is a deep CNN model known for its simplicity and effectiveness, primarily characterized by its use of 3x3 convolutional layers with a stride of 1 and 2x2 max-pooling layers with a stride of 2. The '16' in VGG16 refers to the 16 layers that have learnable weights (13 convolutional layers and 3 fully connected layers).

In this project, we utilize a pre-trained VGG16 model on the ImageNet dataset, employing transfer learning. The convolutional base of the VGG16 model is used as a fixed feature extractor, and new classification layers are added on top. This approach allows the model to leverage the rich feature representations learned from a large dataset, significantly reducing the training time and the amount of data required for our specific task.

After the VGG16 convolutional base, a `GlobalAveragePooling2D` layer is added to reduce the dimensionality of the feature maps. This is followed by a `Dense` layer with 128 units and a ReLU activation function, and a `Dropout` layer for regularization to prevent overfitting. Finally, a `Dense` layer with 5 units (corresponding to the five classes) and a `softmax` activation function is used for the final classification output.

Here's a visual representation of the VGG16 architecture:

![VGG16 Architecture](search_images/ZThUHPPJ2A7n.jpg)




## Training and Validation

The model is trained using the Adam optimizer with a learning rate schedule to ensure optimal convergence. Categorical cross-entropy is used as the loss function, and accuracy is monitored as the primary metric. Early stopping is implemented to prevent overfitting, which monitors the validation accuracy and stops training if it does not improve for a specified number of epochs.

Data augmentation plays a crucial role in enhancing the model's ability to generalize. Techniques such as rotation, shear, zoom, horizontal flips, and shifts in width and height are applied to the training images. This artificially expands the dataset, making the model more robust to variations in the input data.

## Results

The model demonstrates strong performance in classifying the different syndromes. The training process is monitored closely for both training and validation accuracy and loss. The following plots illustrate the model's performance during training:

### Accuracy Plot

![Accuracy Plot](https://private-us-east-1.manuscdn.com/sessionFile/0BWJF58zC109Jd8hnT65A7/sandbox/LdZJsjLL3en3xFoXB9VvQk-images_1753751184570_na1fn_L2hvbWUvdWJ1bnR1L2FjY3VyYWN5X3Bsb3Q.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvMEJXSkY1OHpDMTA5SmQ4aG5UNjVBNy9zYW5kYm94L0xkWkpzakxMM2VuM3hGb1hCOVZ2UWstaW1hZ2VzXzE3NTM3NTExODQ1NzBfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwyRmpZM1Z5WVdONVgzQnNiM1EucG5nIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNzk4NzYxNjAwfX19XX0_&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=ETw3SFob9QT-CpiaS2gBmm~Ie73pPy-F6w1Hgu7me1PTnYvHz25OWQiZlGlTBqJGqn674yxgTxjeOTrVba8kh5jZOF6cOaTNyddpXtNV8ArNFbDQzUnNCMiaqfJhfpzXyTWOnAPctLMc~bU5Gipe-k-O4SCOyYttV3DMLVU9FLN0zoavB7mrOpo6-VE7LRdFLxvZbCGDKTXfi4KsBLwL9cyvx-6du04SOBmYp0jy4cwScp3Jo65yvu1qaHpq2S5es9pPqw4DEGsNuwcfJipW2fepNGyqnb6NCOh5gCLB9gweofK7mSuoKOftZfknzaFxg8BIRbRebuX6ltSv8BwrTg__)

This plot shows the training accuracy and validation accuracy over the epochs. A high and converging validation accuracy indicates that the model is learning effectively and generalizing well to unseen data.

### Loss Plot

![Loss Plot](https://private-us-east-1.manuscdn.com/sessionFile/0BWJF58zC109Jd8hnT65A7/sandbox/LdZJsjLL3en3xFoXB9VvQk-images_1753751184570_na1fn_L2hvbWUvdWJ1bnR1L2xvc3NfcGxvdA.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvMEJXSkY1OHpDMTA5SmQ4aG5UNjVBNy9zYW5kYm94L0xkWkpzakxMM2VuM3hGb1hCOVZ2UWstaW1hZ2VzXzE3NTM3NTExODQ1NzBfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwyeHZjM05mY0d4dmRBLnBuZyIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc5ODc2MTYwMH19fV19&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=pN5R0STM-2C8b87dYA9YLl7vUP9ue~EMsauQlGbxykX0qA7nt1zvRhLGByc~hkXEAdYm5HpwOIYLu2ZhWu4ajBO0HUp5wlnJUnwJqTkJQdICrRdVvoDYoVFq4KRD4aZBXGY3BCgkwEMU7hTTeVQ~FnhHx55~qpsNwy8Vdu3Lkl75cpzl4Sd4r-FfrwYyehtKdf8i9CwoZCWP7TG1s8Qb9gEldK9Fr-Esq9gmRyQ6yFi6ueWL-~GVQa-Imc4UdiOqi5RivsVxZ4eOvmNTxuQsACm3KElHI3sTEXhmKoIva8YTghxv7f9mZurucGTNv-~Dh7ASwSpI-n79nCmIfve2RA__)

This plot displays the training loss and validation loss over the epochs. A decreasing trend in both training and validation loss signifies that the model is learning and minimizing errors.





### Confusion Matrix

![Confusion Matrix](https://private-us-east-1.manuscdn.com/sessionFile/0BWJF58zC109Jd8hnT65A7/sandbox/LdZJsjLL3en3xFoXB9VvQk-images_1753751184571_na1fn_L2hvbWUvdWJ1bnR1L2NvbmZ1c2lvbl9tYXRyaXg.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvMEJXSkY1OHpDMTA5SmQ4aG5UNjVBNy9zYW5kYm94L0xkWkpzakxMM2VuM3hGb1hCOVZ2UWstaW1hZ2VzXzE3NTM3NTExODQ1NzFfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwyTnZibVoxYzJsdmJsOXRZWFJ5YVhnLnBuZyIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc5ODc2MTYwMH19fV19&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=EU7u2q7x7AlM53-t3UeyWWBVrZV~qumgf-a5lSjSUuz8e-wRuPgSne2mfdHpN7ccMEHoUbwHv3-ZTo47lobGb4kZHIbGCddai69qaca59P9oe2FkGtcqzmvj3vw9T13UjVtALqtX0h8kSELkvYOvdgcyE6rKF4GuH32plob3xjHFXp2dABDNVBBwbNsZVqTFjT-Sx-Pze2OrGHyJXmLAT3sufx3tYILs1XFCc9TJHvFK4vrRSg1QzK2L4V4viFza6eV~lQ34XklVvoSYJk6kD3OY8JFzDe1IQBuxW0iA-RdkycKEfVWnAm905UgdeVyhDHtWxmNTgoi3NdqFOp2gUw__)

The confusion matrix provides a detailed breakdown of the model's performance for each class, showing the number of correct and incorrect predictions. This helps in understanding which classes are well-classified and which ones might be challenging for the model.





### Confusion Matrix

![Confusion Matrix](confusion_matrix.png)

The confusion matrix provides a detailed breakdown of the model's performance for each class, showing the number of correct and incorrect predictions. This helps in understanding which classes are well-classified and which ones might be challenging for the model.



