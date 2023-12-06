# Music Emotion Detection with Human-Interpretable Mid-Level Features
<img src="images/Arch.png" width="750" height="250">

## 1. Project context
Our "Song of Storms" production experience confirmed the criticality of ensuring __`machines’ participation won’t affect`__ the __`authenticity`__ and __`artistic integrity`__ of performances’ __`emotional expression`__. Machines’ ability to detect musicians’ __`dynamic emotions`__ is a crucial step, yet very challenging with the traditional __`static rule-based signal processing`__. The use of AI for detecting emotions in music has emerged as a key focus in academic research. __`AI-based emotion detection`__ typically involves training machine learning models, particularly neural networks, on large datasets of music that have been pre-labeled with various emotional states. The process generally includes these steps:
- __Data Collection__: Compile a diverse dataset of music pieces, each annotated with specific emotional labels like happiness, sadness, anger, etc.
- __Feature Extraction__: Analyze and extract features from the music that are relevant to emotion, such as tempo, pitch, rhythm, harmony, and dynamics.
- __Model Training__: Train a machine learning model, such as a neural network, using this labeled dataset. The model learns to associate specific musical features with corresponding emotions.
- __Validation and Testing__: Test the model on a separate set of data to validate its accuracy in predicting emotional content.
- __Application__: Implement the trained model in emotion detection applications.

## 2. Project objective
Excited by AI-powered emotion detection research, I studied an emotion classification algorithm based on a Visual Geometry Group (VGG)-style neural network. By using music's spectrogram representation as input, and training the VGG model to recognize human-interpretable, mid-level perceptual features (e.g., melodiousness, dissonance, and tonal stability, etc.) from the spectrogram, the algorithm can rate emotions by linearly combining the mid-level feature predictions. For instance, the rating of "happy emotion"=0.42x"tonal_stability" + 0.37x"rhythm_complexity" + 0.18x"articulation" - 0.46x"dissonance" - 0.41x"modality" - 0.16x"rhythm_stability". 

## 3. Project details
This section provides a detailed explanation of the AI model, and a step-by-step guide to applying the model for emotion detection.

This project is based on an AI-powered music emotion recognition research paper--[Towards Explainable Music Emotion Recognition: The Route via Mid-level Features](https://arxiv.org/pdf/1907.03572) by S. Chowdhury et al. The model tries to give a musically meaningful and intuitive explanation for its music emotion predictions. A VGG-style deep neural network has been adopted to classify emotional characteristics of a musical piece together with (and based on) human-interpretable, mid-level perceptual features.

### 3.1 Music data preprocessing
<img src="images/Spectogram.png" width="550" height="250">
In terms of preprocessing, audio samples are initially transformed into 149-point spectrograms. These are derived from 10-second segments randomly chosen from the original audio. The samples are resampled at a frequency of 22.05 kHz, with each frame comprising 2048 samples and a frame rate set at 31.25 frames per second. Before creating the logarithmic-scaled spectrogram, the audio's amplitude is normalized. This process produces input vectors with dimensions of 313x149, which are then utilized as inputs for the subsequent model architectures.

### 3.2 Mid-level features
<img src="images/Spectogram2Mid.png" width="750" height="250">

Perceptual mid-level features is defined in [A datadriven approach to mid-level perceptual musical feature modeling](https://arxiv.org/pdf/1806.04903.pdf) by A. Aljanaki et al., along with questions that were provided to human raters to help them interpret the concepts. (The ratings were collected in a pairwise comparison scenario.)

<img src="images/Mid.png" width="550" height="250">

### 3.2 VGG-style neural network
VGGNet was invented by Visual Geometry Group (by Oxford University). This architecture was the 1st runner up of ILSVR2014 in the classification task while the winner is GoogLeNet. This tutorial [Introduction to VGGNet](https://becominghuman.ai/what-is-the-vgg-neural-network-a590caa72643) is a good source if you are interested in the detailed VGG architecture.

<img src="images/VGG.png" width="300" height="350">

### 3.3 Emotion detection architecture
The research explored three distinct methods for emotion modeling in audio, each utilizing VGG-style convolutional neural networks (CNNs). The specifics of these architectures are illustrated in the following figure. Across all models, an Adam optimizer with a learning rate set at 0.0005 and a batch size of 8 was employed. Additionally, to mitigate overfitting, early stopping was implemented, set to trigger after 50 epochs without improvement.

<img src="images/VGG4All.png" width="300" height="500">

- __"A2E"__: The simplest approach, where spectrograms are directly fed into a VGG-style CNN to predict emotion values from audio. This is depicted as the leftmost path in the figure.
- __"A2Mid2E"__: Aimed at achieving a more interpretable model, this middle path uses a VGG-style network to first predict mid-level features from audio, followed by a linear regression model that predicts 8 emotion ratings from 7 mid-level feature values. This corresponds to a fully connected layer with 7 inputs and 8 outputs.
- __"A2Mid2E-Joint"__: The rightmost path in the figure, this model jointly learns to predict mid-level features and emotion ratings. It predicts emotions directly from the mid-level features through a linear layer. The network yields two outputs: one from the penultimate "mid-level layer" and another from the final "emotion layer." Both outputs' losses are calculated, and the combined loss (their summation) is optimized.

The following figure illustrates the key concept of mapping mid-level features to emotions (happy, sad, tender, fearful, angry, valence, energy, tension). For instance, the rating of "emotion of happiness"=0.42x"tonal_stability" + 0.37x"rhythm_complexity" + 0.18x"articulation" - 0.46x"dissonance" - 0.41x"modality" - 0.16x"rhythm_stability". With this mapping, explainability is achieved because one can relate the emotion score to the 7 human-interpretable mid-level features.

__For example, an excess of dissonance in a musical composition tends to result in a low happiness score, which is logically consistent.__

<img src="images/Mid2Emotion.png" width="550" height="270">

### 3.4 Mid-level features to emotion score mapping results
The paper compares the three model architectures (A2E, A2Mid2E, A2Mid2E-Joint) on the full task of predicting emotion from audio. The A2E model serves as reference for the subsequent models with explainable linear layers. The results can be found in the table below.

<img src="images/MappingScore.png" width="650" height="130">

The key conclusion is A2Mid2E-Joint comes very close to the reference model of A2E, with just 0.01 drop in accuracy in exchange for explainability. Hence I have decided to choose both A2E and A2Mid2E-Joint for my experimentations.

### 3.5 Datasets used
For the datasets, we utilized Aljanaki & Soleymani's [Mid-level Perceptual Features dataset](https://osf.io/5aupt/) for mid-level feature annotations. For the emotion prediction experiments, the [Music and emotion stimulus dataset](https://osf.io/p6vkg/) was employed. This dataset includes a collection of music and participants ratings of emotions for a selected short clips of film soundtracks that have been used to study emotion recognition and induction in music ([A comparison of the discrete and dimensional models of emotion in music. Psychology of Music, 39(1), 18-49](https://doi.org/10.1177/0305735610362821), Eerola and Vuoskoski, 2011).

### 3.6 Training
To be updated soon with Python codes.

### 3.5 Inference experiments
To be updated soon with Python codes & results showing nearly 80% accuracy across various music pieces.
