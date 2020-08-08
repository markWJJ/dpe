# Dynamic Programming Encoding for Subword Segmentation in Neural Machine Translation

## Descriptions
This repo contains source code and pre-processed corpora for Dynamic Programming Encoding (DPE) for Subword Segmentation in Neural Machine Translation (accepted to ACL2020) ([paper](https://arxiv.org/abs/2005.06606))


## Dependencies
* python3
* [fairseq](https://github.com/pytorch/fairseq) (commit: 58b912f)
* pytorch1.1
* [sentencepiece](https://github.com/google/sentencepiece)
* cuda 10.0
 
## Data Preparation
* Using any tokenizer (we use [MOSES toolkit](https://github.com/moses-smt/mosesdecoder)) to tokenize your corpus 
* Using sentencepiece (bpe mode) to segment your tokenized corpus (you can refer to `seg_data.py`)
* Using fariseq to construct your bpe dictionary: dict.{src}.txt dict.{tgt}.txt
* Constructing your char dictionary: dict.{tgt}.in.txt (you can refere to `build_dict.py`)
* Keep your dataset in plain text format: {train/valid/test}.src-tgt.{src/tgt}, where src and tgt are your source and target language pairs respectively

## Training
To train a DPE segmenter
```shell
# SRC: source language
# TGT: target language
# SEED: a seed for reproducibility
sh run_batch SRC TGT SEED
```

## MAP Inference
To segment a corpus
```shell
# SRC: source language
# TGT: target language
# SEED: a seed for reproducibility
sh seg_batch.sh SRC TGT SEED
```

## Machine Translation
Once your corpus is segmented, you can use your favourite MT toolkit to train a MT system. We use fairseq for our experiments.
* source sentences can be segmented by one of the following segmentation algorithms:
    - bpe
    - unigram
    - bpe-droput
    - dpe
* target sentences are dpe segmented

## Segmented Corpora
* [en-de (WMT14)](https://drive.google.com/file/d/1BxaHJGkJ4vRFuhPno3DMtcVWBI4aC8bh/view?usp=sharing)
* [en-fi (WMT15)](https://drive.google.com/file/d/1J7uX5TQ2ivMowLWFmZrYrtJ47DeEWG2Q/view?usp=sharing)
* [en-et (WMT18)](https://drive.google.com/file/d/1Z9azC-FGJABmxTo29P46BhwNsCbaRu9P/view?usp=sharing)
