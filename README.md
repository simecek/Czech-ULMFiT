# ULMFiT for Czech

## Intro

To paraphrase a [Machine Learning Explained](https://mlexplained.com/2019/06/30/paper-dissected-xlnet-generalized-autoregressive-pretraining-for-language-understanding-explained/) blog: 2018 was an NLP breakthrough year. Most of the advances centered around **language modeling** and **transfer learning**. 

**Language modeling** is a fancy word for the task of predicting the next word in a sentence given all previous words. The advantage is that you can train a language model on a large unlabeled corpus, such as Wikipedia.

You can then try to **transfer** the collected knowledge to another task, like text classification.  

## ULMFiT

ULMFiT paper appeard in January 2018 and was the pioneer of this trend. ULMFit runs in three steps: *first*, train a language model, *then* fine-tune it to a specific task and *finally* use the fine-tuned model for the final prediction. The method is described in the following paper and implemented in [fastai package](https://docs.fast.ai/).

📝 [Howard, Jeremy, and Sebastian Ruder. "Universal language model fine-tuning for text classification." arXiv preprint arXiv:1801.06146 (2018).](https://arxiv.org/abs/1801.06146)

Slavic and other morphologically rich languages need a special preprocessing ([sentencepiece](https://github.com/google/sentencepiece) instead of spaCy) as explained in the following paper for Polish.

📝 [Czapla, Piotr, Jeremy Howard, and Marcin Kardas. "Universal Language Model Fine-Tuning with Subword Tokenization for Polish." arXiv preprint arXiv:1810.10222 (2018).](https://arxiv.org/abs/1810.10222)

## ULMFiT Language Model for the Czech

Notebook(s): [nn-czech.ipynb](language_model/nn-czech.ipynb)

Weights: [cs_wt.pth](https://drive.google.com/open?id=14b5x5r3x5MeZNZ8Uc4L3ZmiHAiDgKNj2), [cs_wt_vocab.pkl](https://drive.google.com/open?id=1NZym3XfEWAGJ7L3O56Zk2er6bwjKdJGe), [spm.model](language_model/spm.model), [spm.vocab](language_model/spm.vocab)

To my knowledge, this is **the first ULMFit language model for Czech**. With P4 Tesla GPU and Google Cloud virtual machine specified [here](https://course.fast.ai/start_gcp.html), the training took ~28 hours. I was closely following the recent [ULMFit lecture from fast.ai NLP course](https://www.youtube.com/watch?v=MDX_x6rKXAs&list=PLtmWHNX-gukKocXQOkQjuVxglSDYWsSh9&index=10).

## Experiments

The experiments are still a work in progress (*help needed! do you know any good Czech sentiment benchmark?*). I have found a couple of datasets in the following paper: 

📝 [Habernal, Ivan, Tomáš Ptáček, and Josef Steinberger. "Sentiment analysis in czech social media using supervised machine learning." Proceedings of the 4th workshop on computational approaches to subjectivity, sentiment and social media analysis. 2013.](https://www.aclweb.org/anthology/W13-1609)

Data: http://liks.fav.zcu.cz/sentiment/ ([Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported License](https://creativecommons.org/licenses/by-nc-sa/3.0/))

As a proof of concept, I have performed sentiment classification of ~60K Czech movie reviews: 

1) **CSFD movie dataset**: 91,381 movie reviews (30,897 positive, 30,768 neutral, and 29,716 negative reviews) from the [Czech Movie Database](https://www.csfd.cz/). In this first experiment, I omitted neutral reviews and made a classifier of positive vs. negative reviews only (90% used for training, 10% for validation). The achieved accuracy was **94.5%**. 

Notebook(s): [nn-czech.ipynb](language_model/nn-czech.ipynb) (same as for language model training)

## Acknowledgments

This repo is a little dwarf standing on the shoulder of giants. Let me thank at least a few of them:

* Jeremy Howard, Rachel Thomas and the whole fast.ai team for ULMFit developement and making an addition of new languages super simple with the last fastai version. Also, Piotr Czapla for subword tokenization idea and the Polish ULMFit model.

* Karla Fejfarova for introducing me to ULMFit a year ago. Katerina Veselovska for a motivation after her recent NLP talk at ML meetup in Brno.

* Google for free Google Cloud credits.
