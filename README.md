# Automatic Video Dubbing system from English to Arabic  

This project presents a comprehensive study on video dubbing techniques and the development of a specialized video dubbing system. The objective is to replace the original voices in foreign language videos with the voices of performers speaking the language of the target audience, while ensuring synchronization between lip movements and the dubbed speech.

## Importance of Automatic Video Dubbing

Video dubbing aims to make video content invariant across worldwide cultures. Automatic video dubbing systems typically involve three sub-tasks:

- Automatic Speech Recognition (ASR), which transcribes the original speech into text in the source language.
- Neural Machine Translation (NMT), which translates the source language text to the target language  
- Text-to-Speech (TTS), which synthesizes the translated text into target speech.  

Video dubbing enhances accessibility, engagement, and global distribution of multilingual content while preserving visual integrity for cross-cultural communication.  

## Challenges

Automatic video dubbing faces several challenges:

- Lip sync accuracy
- Naturalness of dubbed voice
- Cultural adaptation and localization
- Multilingual and multicultural considerations
- Code switching.

## Methodology  

Dubbing Process
![Ai part for dubbing](assests/ai%20pip.png)

Speech Translator
![Translator Block](assests/ai%20in%20depth.png)

The proposed methodology involves:

1. Separating the audio and video from the source English video
2. Translating the English audio to Arabic speech using a speech translator
3. Preserving the original video frames
4. Merging the translated Arabic speech with the video frames to create an Arabic dubbed video

To improve the results, two additional models are used in speech translator:

- Punctuation model to add punctuation to English subtitles
- Tashkeel model to add diacritical marks to Arabic text

## System Architecture

![Alt text](assests/image2.png)

The system follows a modular architecture consisting of:

- User facing apps (Flutter app)

- Application server (localhost and herouku)

- Database server (firebase)

- Machine learning pipelines for ASR, NMT, TTS (Pytorch, Tensorflow and HuggingFace)

The application server handles user management, video uploads/downloads, and interfacing with the ML pipelines. The database stores user data, video metadata, transcripts etc.

## Speech Recognition

![as](assests/Picture1.jpg)

- Experiments compared Wave2Vec2.0 and Google Speech Recognition APIs.

- Wave2Vec2.0 gave lower Word Error Rates by pretraining on large unlabeled speech data followed by finetuning on a small labeled dataset.

- CTC loss function used to train acoustic model to convert speech features into character probabilities.

## Machine Translation

![Alt text](assests/image.png)

Google's NMT architecture utilizes LSTM layers with attention mechanism:

- Encoder LSTM converts source text into vector representations
- Attention module aligns source representations to each target word
- Decoder LSTM predicts target words sequentially based on context vectors

Key optimizations include:

1) Byte-pair encoding of words into subwords to handle rare words
2) Residual connections in stacked LSTM layers to improve gradient flow
3) Beam search decoding to reduce errors and find optimal translations

## Text to Speech

![fd](assests/Picture2.png)

1. FastSpeech2 is a non-autoregressive neural TTS model, allowing faster synthesis compared to autoregressive models like WaveNet during inference.
2. The model takes text as input and predicts mel-spectrogram acoustic features using a Transformer encoder-decoder architecture.
3. Instead of dilated convolutions, multi-layer perceptrons (MLPs) with convolutional processing are used in the model architecture. This provides local feature modeling.
4. Additional variance predictors are incorporated to model speech attributes like pitch, duration and energy profiles. This improves prosody and naturalness.

In summary, the key aspects are:

- Non-autoregressive parallel synthesis
- Transformer encoder-decoder
- MLP layers for local context
- Variance predictors capture speech profiles

This allows FastSpeech2 to generate high quality mel-spectrograms from text in parallel during inference while maintaining natural prosody and voice characteristics.

## Results

Based on the subjective evaluations done as part of the testing process, some of the key areas identified for further improvement in translation and dubbing quality were:

- Lip synchronization: More work needed to finely tune the timing and duration of dubbed speech to better match lip movements.

- Expression: Capturing the emotion and emphasis in the original speech through appropriate intonation and prosody in the dubbed speech.

- Fluency: Some unnaturalness detected in the translated Arabic speech in terms of fluidity of sentences.

- Terminology: Domain-specific vocabulary posed challenges, especially technical jargon. Performance decreased for specialized domains.

- Speaker similarity: While multiple speaker models were created, more personalization is required to better mimic the original speaker voice.

- Background noise: Reduction of background artifacts and improvement of audio clarity for the dubbed speech.

- Grammar: Better grammatical analysis during translation required to produce perfectly coherent Arabic sentences.

- Dialectal speech: Handling informal language, dialects and slang terms needs more sophisticated capabilities.

So in summary, the areas requiring additional enhancements are: synchronization, emotion/emphasis, fluency, terminology, speaker similarity, audio quality, grammar, and dialectal speech. Addressing these areas through better datasets, customized models and training techniques would further boost the translation and dubbing accuracy.

## Conclusion

The project demonstrates the potential of video dubbing technology to increase accessibility to multimedia content and bridge language gaps. However, there are opportunities for enhancing dubbing accuracy, voice recognition, audio quality, and feature expansion in future work.