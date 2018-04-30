# OMGEmotionChallenge code

## Dependencies
- python3.6
- tensorflow
- keras
- anaconda3
- sklearn

> Please use the latest version without additional explanations

## Submission

### 1. Single Multi-modality Model (S1)
In this model, we use visual and acoustic features.

To build the model for valence prediction, we use only visual features. The visual features are constructed in the following way (Visual Extractor 1, VE1): the face region is first detected and cropped by seeta-face without alignment. We then use the VGG-face network to extract visual representations. The representations are passed through a LSTM network with attention layer to get the context-aware visual representations. We take MAE (mean absolute error) as our loss function. Besides, temporal data augmentation is made by randomly selecting frames in each time window.

To build the model for arousal prediction, we use both visual and acoustic features. The Visual Extractor 2 (VE2) is built in a similar way as VE1. The only difference is that the LSTM module is replaced by a 1D-CNN structure. The acoustic features are extracted using OpenSmile (Acoustic Extractor 1, AE1). And we use feature selection algorithm to reduce the dimensionality of acoustic features.

The visual and acoustic representations are passed into a SVM classifier to make the final predictions.

### 2. The Ensemble Model I
The model is made up by two single models. One is the single model S1 described in submission 1. The second single model (S2) is described below.

Different from model S1, where the arousal and valence predictions use different features, in model S2 the arousal and valence predictions are made based on the same features. We combine VE1, VE2, AE1 and another acoustic extractor (AE2) using SoundNet. The visual and acoustic representations are passed into a SVM classifier to make the final predictions.

The final predictions are simply generated by a weighted sum of model S1 and model S2 predictions.

### 3. The Ensemble Model II
The model is made up by three single models. The first two models are S1 and S2. The third single model S3 is described below.

In model S3, We only make use of visual features. The feature extractor is similar to VE1 except we train the CNN and LSTM altogether.

The final predictions are simply generated by a weighted sum of model S1, S2 and S3 predictions.
