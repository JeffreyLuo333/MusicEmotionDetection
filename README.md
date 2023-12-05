# Music Emotion Detection with Human-Interpretable Mid-Level Features
<img src="images/Arch.png" width="750" height="250">

## 1. Project context
The "Song of Storms" production experience revealed the vital role of __`human-machine synergy`__ in crafting __`humane audience experiences`__. Real-time __`synchronization`__ of __`machines' sounds`__ with musicians' __`dynamic emotions`__ is crucial yet presents challenges with the traditional __`static rule-based signal processing`__. Applying AI to detect emotions in music has become one of the main approaches in academic research. __`AI-based emotion detection`__ typically involves training machine learning models, particularly neural networks, on large datasets of music that have been pre-labeled with various emotional states. The process generally includes these steps:
- __Data Collection__: Compile a diverse dataset of music pieces, each annotated with specific emotional labels like happiness, sadness, anger, etc.
- __Feature Extraction__: Analyze and extract features from the music that are relevant to emotion, such as tempo, pitch, rhythm, harmony, and dynamics.
- __Model Training__: Train a machine learning model, such as a neural network, using this labeled dataset. The model learns to associate specific musical features with corresponding emotions.
- __Validation and Testing__: Test the model on a separate set of data to validate its accuracy in predicting emotional content.
- __Application__: Implement the trained model in emotion detection applications.

## 2. Project objective
Excited by AI-powered emotion detection research, I studied an emotion classification algorithm based on a Visual Geometry Group (VGG)-style neural network. By using music's spectrogram representation as input, and training the VGG model to recognize human-interpretable, mid-level perceptual features (e.g., melodiousness, dissonance, and tonal stability, etc.) from the spectrogram, the algorithm can rate emotions by linearly combining the mid-level feature predictions. For instance, the rating of happy emotion=0.42xtonal_stability + 0.37xrhythm_complexity + 0.18xarticulation - 0.46xdissonance - 0.41xmodality - 0.16xrhythm_stability. 





My experimentation with various music has yielded close to 80% classification accuracy.




https://becominghuman.ai/what-is-the-vgg-neural-network-a590caa72643
