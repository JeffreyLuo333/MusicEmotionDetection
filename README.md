# Music Emotion Detection with Human-Interpretable Mid-Level Features

## 1. Project context
The "Song of Storms" production experience revealed the vital role of human-machine synergy in crafting humane audience experiences. Real-time synchronization of machines' sounds with musicians' dynamic emotions is crucial yet presents challenges with the traditional static rule-based signal processing. 

## 2. Project objective
Excited by AI-powered emotion detection research, I studied an emotion classification algorithm based on a VGG-style neural network. By using music's spectrogram representation as input, and training the VGG model to recognize human-interpretable, mid-level perceptual features (e.g., melodiousness, dissonance, and tonal stability, etc.) from the spectrogram, the algorithm can rate emotions by linearly combining the mid-level feature predictions. For instance, the rating of happy emotion=0.42*tonal_stability + 0.37*rhythm_complexity + 0.18*articulation - 0.46*dissonance - 0.41*modality - 0.16*rhythm_stability. My experimentation with various music has yielded close to 80% classification accuracy.
Excited by AI-powered emotion detection research, I studied an emotion classification algorithm based on a VGG-style neural network. By using music's spectrogram representation as input, and training the VGG model to recognize human-interpretable, mid-level perceptual features (e.g., melodiousness, dissonance, and tonal stability, etc.) from the spectrogram, the algorithm can rate emotions by linearly combining the mid-level feature predictions. For instance, the rating of happy emotion=0.42*tonal_stability + 0.37*rhythm_complexity + 0.18*articulation - 0.46*dissonance - 0.41*modality - 0.16*rhythm_stability. My experimentation with various music has yielded close to 80% classification accuracy.



https://becominghuman.ai/what-is-the-vgg-neural-network-a590caa72643
