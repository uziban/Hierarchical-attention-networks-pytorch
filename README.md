# [PYTORCH] Hierarchical Attention Networks for Document Classification

## Introduction

Here is my pytorch implementation of the model described in the paper **Hierarchical Attention Networks for Document Classification** [paper](https://www.cs.cmu.edu/%7Ediyiy/docs/naacl16.pdf). 

<p align="center">
  <img src="demo/video.gif"><br/>
  <i>An example of my model's output for Dbpedia dataset.</i>
</p>

## Datasets:

Statistics of datasets I used for experiments. These datasets could be download from [link](https://drive.google.com/drive/u/0/folders/0Bz8a_Dbh9Qhbfll6bVpmNUtUcFdjYmF2SEpmZUZUcVNiMUw1TWN6RDV3a0JHT3kxLVhVR2M)

| Dataset                | Classes | Train samples | Test samples |
|------------------------|:---------:|:---------------:|:--------------:|
| AG’s News              |    4    |    120 000    |     7 600    |
| Sogou News             |    5    |    450 000    |    60 000    |
| DBPedia                |    14   |    560 000    |    70 000    |
| Yelp Review Polarity   |    2    |    560 000    |    38 000    |
| Yelp Review Full       |    5    |    650 000    |    50 000    |
| Yahoo! Answers         |    10   |   1 400 000   |    60 000    |
| Amazon Review Full     |    5    |   3 000 000   |    650 000   |
| Amazon Review Polarity |    2    |   3 600 000   |    400 000   |

Additionally, I also use word2vec pre-trained models, taken from GLOVE, which you could download from [link](https://nlp.stanford.edu/projects/glove/). I run experiments with all 4 word2vec files (50d, 100d, 200d and 300d). You could easily switch to other common word2vec models, like the one provided in FastText [link](https://fasttext.cc/docs/en/crawl-vectors.html) 
In the paper, it is said that a pre-trained word2vec is used. however, to the best of my knowledge, at least in pytorch, there is no implementation on github using it. In all HAN github repositories I have seen so far, a default embedding layer
was used, without loading pre-trained word2vec model. I admit that we could still train HAN model without any pre-trained word2vec model. However, to serve the purpose of re-implementing origin model, in all experiments, ad mentioned above, I used 1 out of 4 pre-trained word2vec models as initilization for embedding layer.

## Setting:

During my experiments, I found out that given different datasets and different embedding layer's dimension, some combinations of batch size and learning rate yield better performance (faster convergence and higher accuracy) than others. Particularly in some cases, if you set wrong values for these 2 very important parameters, your model will never converge. Detail setting for each experiments will be shown in **Experiments** part.
I have not set a fixed number of epoches for each experiment. Instead, I apply early stopping technique, to stop training phase after validation loss has not been improved for **n** epoches. 

## Training

If you want to train a model with default parameters, you could run:
- **python train.py**

If you want to train a model with your preference parameters, like optimizer and learning rate, you could run:
- **python train.py --batch_size batch_size --lr learning_rate**: For example, python train.py --batch_size 512 --lr 0.01

If you want to train a model with your preference word2vec model, you could run:
- **python train.py --word2vec_path path/to/your/word2vec**

## Test

For testing a trained model with your test file, please run the following command:
- **python test.py --word2vec_path path/to/your/word2vec**, with the word2vec file is the same as the one you use in training phase.

You could find some trained models I have trained in [link](https://drive.google.com/open?id=1zzC4r0nn8yInWjCbVrVZPFYyOWJQizqh)

## Experiments:

Results for test set are presented as follows:  A(B/C):
- **A** is accuracy.
- **B** is learning rate used.
- **C** is batch size.

Each experiment is run over 10 epochs.

|      Size     |        50      |      100     |      200     |      300     |
|:---------------:|:------------------:|:------------------:|:------------------:|:------------------:|
|    ag_news    |   updated soon   |   updated soon   |   updated soon   |   updated soon   |
|   sogu_news   |   updated soon   |   updated soon   |   updated soon   |   updated soon   |
|    db_pedia   |   updated soon   |   updated soon   |   updated soon   |   updated soon   |
| yelp_polarity |   updated soon   |   updated soon   |   updated soon   |   updated soon   |
|  yelp_review  |   updated soon   |   updated soon   |   updated soon   |   updated soon   |
|  yahoo_answer |   updated soon   |   updated soon   |   updated soon   |   updated soon   |
| amazon_review |   updated soon   |   updated soon   |   updated soon   |   updated soon   |
|amazon_polarity|   updated soon   |   updated soon   |   updated soon   |   updated soon   |

The training/test loss/accuracy curves for each dataset's experiments (with the order from left to right, top to bottom is 50d, 100d, 200d and 300d word2vec) are shown below:

- **ag_news**

<img src="demo/agnews_50.png" width="450"> <img src="demo/agnews_100.png" width="450"> 
<img src="demo/agnews_200.png" width="450"> <img src="demo/agnews_300.png" width="450">


