# GigaAM: the family of open-source acoustic models for speech processing

![plot](./gigaam_scheme.svg)

## Table of contents

* [GigaAM](#gigaam)
* [GigaAM for Speech Recognition](#gigaam-for-speech-recognition)
  * [GigaAM-CTC](#gigaam-ctc)
  * [GigaAM-RNNT](#gigaam-rnnt)
* [GigaAM-Emo](#gigaam-emo)
* [License](./GigaAM%20License_NC.pdf)
* [Links](#links)

## GigaAM

GigaAM (**Giga** **A**coustic **M**odel) is a [Conformer](https://arxiv.org/pdf/2005.08100.pdf)-based [wav2vec2](https://arxiv.org/pdf/2006.11477.pdf) foundational model (around 240M parameters). We trained GigaAM on nearly 50 thousand hours of diversified speech audio in the Russian language.

Resources:
* [Model weights](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/ssl_model_weights.ckpt)
* [Encoder config](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/encoder_config.yaml)
* [Colab example](https://colab.research.google.com/github/salute-developers/GigaAM/blob/main/examples/notebooks/GigaAM_Model_Usage_Example.ipynb)
* [Docker example](./examples/README.md)


## GigaAM for Speech Recognition

We fine-tuned the GigaAM encoder for Speech Recognition with two different decoders:
* GigaAM-CTC was fine-tunined with [Connectionist Temporal Classification](https://www.cs.toronto.edu/~graves/icml_2006.pdf) and character-based tokenizer.
* GigaAM-RNNT was fine-tuned with [RNN Transducer loss](https://arxiv.org/abs/1211.3711) and subword tokenizer.

Both models were trained using [the NeMo toolkit](https://github.com/NVIDIA/NeMo) on publicly available Russian labeled data:

| dataset | size, hours | weight |
| --- | --- | --- |
| [Golos](https://arxiv.org/pdf/2106.10161.pdf) | 1227 | 0.6 |
| [SOVA](https://github.com/sovaai/sova-dataset) | 369 | 0.2 |
| [Russian Common Voice](https://arxiv.org/pdf/1912.06670.pdf) | 207 | 0.1 |
| [Russian LibriSpeech](https://arxiv.org/pdf/2012.03411.pdf) | 93 | 0.1 |


Resources:
* ### GigaAM-CTC:
  * [Model weights](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/ctc_model_weights.ckpt)
  * [Model config](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/ctc_model_config.yaml)
  * [Colab example](https://colab.research.google.com/github/salute-developers/GigaAM/blob/main/examples/notebooks/GigaAM_CTC_Model_Usage_Example.ipynb)
  * [Docker example](./examples/README.md)
* ### GigaAM-RNNT:
  * [Model weights](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/rnnt_model_weights.ckpt)
  * [Model config](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/rnnt_model_config.yaml)
  * [Colab example](https://colab.research.google.com/github/salute-developers/GigaAM/blob/main/examples/notebooks/GigaAM_RNNT_Model_Usage_Example.ipynb)
  * [Docker examples](./examples/README.md)

The following table summarizes the performance of different models in terms of Word Error Rate on open Russian datasets:

| model | parameters | [Golos Crowd](https://arxiv.org/abs/2106.10161) | [Golos Farfield](https://arxiv.org/abs/2106.10161) | [OpenSTT Youtube](https://github.com/snakers4/open_stt) | [OpenSTT Phone calls](https://github.com/snakers4/open_stt) | [OpenSTT Audiobooks](https://github.com/snakers4/open_stt) | [Mozilla Common Voice](https://arxiv.org/pdf/1912.06670.pdf) | [Russian LibriSpeech](https://arxiv.org/pdf/2012.03411.pdf) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [Whisper-large-v3](https://huggingface.co/openai/whisper-large-v3) | 1.5B | 17.4 | 14.5 | 21.1 | 31.2 | 17.0 | 5.3 | 9.0 |
| [NVIDIA Ru-FastConformer-RNNT](https://huggingface.co/nvidia/stt_ru_fastconformer_hybrid_large_pc) | 115M | 2.6 | 6.6 | 23.8 | 32.9 | 16.4 | 2.7 | 11.6 |
| GigaAM-CTC | 242M | 3.1 | 5.7 | 18.4 | 25.6 | 15.1| 1.7 | 8.1 |
| GigaAM-RNNT | 243M | <span style="color:green">2.3</span> | <span style="color:green">4.4</span> | <span style="color:green">16.7</span> | <span style="color:green">22.9</span> | <span style="color:green">13.9</span> | <span style="color:green">0.9</span> | <span style="color:green">7.4</span> |

## GigaAM-Emo

GigaAM-Emo is an acoustic model for Emotion Recognition. We fine-tuned the GigaAM Encoder on the [Dusha](https://arxiv.org/pdf/2212.12266.pdf) dataset.

Resources:
* [Model weights](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/emo_model_weights.ckpt)
* [Model config](https://n-ws-q0bez.s3pd12.sbercloud.ru/b-ws-q0bez-jpv/GigaAM/emo_model_config.yaml)
* [Colab example](https://colab.research.google.com/github/salute-developers/GigaAM/blob/main/examples/notebooks/GigaAM_Emo_Model_Usage_Example.ipynb)
* [Docker example](./examples/README.md)

The following table summarizes the performance of different models on the [Dusha](https://arxiv.org/pdf/2212.12266.pdf) dataset:

|  |  | Crowd |  |  | Podcast |  |
| --- | --- | --- | --- | --- | --- | --- |
|  | Unweighted Accuracy | Weighted Accuracy | Macro F1-score | Unweighted Accuracy | Weighted Accuracy | Macro F1-score |
| [DUSHA](https://arxiv.org/pdf/2212.12266.pdf) baseline <br/> ([MobileNetV2](https://arxiv.org/abs/1801.04381) + [Self-Attention](https://arxiv.org/pdf/1805.08318.pdf)) | 0.83 | 0.76 | 0.77 | 0.89 | 0.53 | 0.54 |
| [АБК](https://aij.ru/archive?albumId=2&videoId=337) ([TIM-Net](https://arxiv.org/pdf/2211.08233.pdf)) | 0.84 | 0.77 | 0.78 | <span style="color:green">0.90</span> | 0.50 | 0.55 |
| GigaAM-Emo | <span style="color:green">0.90</span> | <span style="color:green">0.87</span> | <span style="color:green">0.84</span> | <span style="color:green">0.90</span> | <span style="color:green">0.76</span> | <span style="color:green">0.67</span> |

## Links
* [[habr] GigaAM: класс открытых моделей для обработки звучащей речи](https://habr.com/ru/companies/sberdevices/articles/805569)
* [[youtube] GigaAM: Семейство акустических моделей для русского языка](https://youtu.be/PvZuTUnZa2Q?t=26442)
* [[youtube] Speech-only Pre-training: обучение универсального аудиоэнкодера](https://www.youtube.com/watch?v=ktO4Mx6UMNk)
