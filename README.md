
# Text to Speech Synthesis

In this project, I have built a text-to-speech system capable of producing accented speech. This system has the capability to generate speech in the style of a selected speaker, with the added ability to convert the speech to a target accent of the user's choice.


## Architecture
The following diagram illustrates the design of the proposed method.

![](https://github.com/shauryat1298/Text-To-Speech-Project/blob/main/images/ar1.png?raw=true)

The proposed method includes Tacotron2 and a Posterior Encoder. The Posterior Encoder utilizes a CVAE (Conditional Variational Autoencoder) architecture in order to maximize the evidence lower bound (ELBO) of the marginal log-likelihood of the data, which is otherwise difficult to calculate.

The CVAE architecture is demonstarated by the following:

![](https://github.com/shauryat1298/Text-To-Speech-Project/blob/main/images/ar2.png?raw=true)

The proposed CVAE encoder has two variations. 

1. The first variation follows the traditional CVAE approach of using labels as conditions for both the encoder and decoder. The idea is that the speaker and accent are primarily determined by the provided labels, while the latent distribution captures finer differences within these categories, such as prosody.
2. The second variation uses labels only in the encoder, so the entire accent and speaker representation is captured by the latent variables za for accent and zs for speaker.

These two variations are referred to as CVAE-L (for 'label') and CVAE-NL ('no-label')
## Dataset used:

In our experiments, we utilize the L2Arctic dataset [18] which consists of 27 hours of recorded speech from 24 speakers speaking in 6 different accents - Arabic, Chinese, Hindi, Korean, Spanish, and Vietnamese. Each accent is represented by two male and two female speakers, and the data is largely parallel except for a few missing utterances in some speakers.
## Results

To evaluate the mel spectrogram reconstruction ability of each model, we use Mel Cepstral Distortion (MCD). Word Error Rate (WER) is used to assess the intelligibility of the synthesized speech. To calculate WER, we utilize pre-trained silero speech-to-text models.

![](https://github.com/shauryat1298/Text-To-Speech-Project/blob/main/images/results.png?raw=true)

I achieved MCD of 7.1 and WER of 0.25 for No-label model, and MCD of 6.98 and WER of 0.24 for label model, outperforming GMVAE, GST and GT models. The results show that all of the models perform similarly in terms of MCD and WER. The proposed CVAE-NL and CVAE-L methods show slightly better performance in terms of MCD.