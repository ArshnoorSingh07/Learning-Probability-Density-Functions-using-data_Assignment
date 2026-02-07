
# Learning Probability Density Functions Using GAN

## 1. Introduction

This project focuses on learning an unknown probability density function (PDF) of a transformed random variable using a Generative Adversarial Network (GAN).  
No analytical or parametric form of the probability distribution is assumed. The density is learned implicitly using samples only.

The dataset used is the India Air Quality Dataset, and NO₂ concentration is selected as the input feature.

---

## 2. Dataset Description

- Dataset Name: India Air Quality Data  
- Source: Kaggle  
- Feature Used: NO₂ concentration  
- Preprocessing:
  - Removal of missing values
  - Normalization of transformed samples for stable GAN training

---

## 3. Methodology

#### Data Collection → Data Preprocessing → Transformation →  GAN Training → Sample Generation → PDF Estimation → Result Analysis

### Step-wise Explanation

1. Data Collection  
   NO₂ concentration values are extracted from the dataset.

2. Transformation  
   The original random variable x is transformed into z using a nonlinear transformation dependent on the roll number.

3. GAN Training  
   A Vanilla GAN is trained using only samples of the transformed variable z, without assuming any analytical PDF.

4. Sample Generation  
   After training, the generator produces new samples from random noise.

5. PDF Estimation  
   Kernel Density Estimation (KDE) is used to estimate PDFs from real and generated samples.

---

## 4. Transformation Parameters

The transformation applied to the random variable is:

z = x + a_r sin(b_r x)

Where:
- r is the university roll number
- a_r = 0.5 × (r mod 7)
- b_r = 0.3 × ((r mod 5) + 1)

### Values Used

- Roll Number (r): 102317161
- a_r = 1.0  
- b_r = 0.6  

Final Transformation:

z = x + 1.0 sin(0.6x)

---

## 5. GAN Architecture Description

### Generator
- Input: Random noise sampled from a standard normal distribution
- Architecture:
  - Fully connected layers
  - ReLU activation in hidden layers
- Output: Generated samples of z

### Discriminator
- Input: Real or generated z samples
- Architecture:
  - Fully connected layers
  - ReLU activation in hidden layers
  - Sigmoid activation in the output layer
- Output: Probability of a sample being real

Training is performed using mini-batch gradient descent with shuffled batches.

---

## 6. PDF Plot Obtained from GAN Samples

After training:
- A large number of samples are generated using the trained generator
- Kernel Density Estimation (KDE) is applied
- The estimated PDF from GAN samples is compared with the real PDF

---

## 7. Graphs and Visual Results


### PDF Comparison Plot

Example:
![PDF Comparison](graph.png)


---

## 8. Observations

### Mode Coverage
The GAN captures the dominant mode of the transformed distribution and covers the main support of the data.

### Training Stability
Training remains stable due to normalization and proper mini-batch training. No severe mode collapse was observed.

### Quality of Generated Distribution
The generated distribution closely follows the real distribution, with minor deviations in low-density tail regions.

---

## 9. Conclusion

This project demonstrates that Generative Adversarial Networks can effectively learn unknown probability density functions using samples alone, without assuming any analytical form.


