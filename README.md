# Peirce computational stylistics
Some code for an on-going analysis of CS Peirce's works by computational stylistics, performed by Luca Pezzini and Bea Somà. 

## The good, the effective and the ugly
This part of the analysis focuses on the strangeness of Peircean terminology and on the repetition of technical terms. [Here]() is the full paper. 

Cite as:
```
@article{pezzini_soma_2026_peirce,
author = {Pezzini, Luca and Somà, Beatrice},
title = {The good, the effective and the ugly. Computational insights into the philosophical style of C.S. Peirce},
year = {2026},
addendum = {accepted for publication}
}
```

We extracted a [sample of ~1000 technical terms by CS Peirce](https://github.com/lucapezzini/peirce_computational_stylistics/blob/main/peirce_technical_terms_CP.txt). They are (a) terms of the Collected Papers which occurr as entries in the [Commens Dictionary](http://www.commens.org/dictionary/), (b) technical terms which are italicized in the Collected Papers, automatically extracted and hand-checked to exclude titles, emphasis and foreign words, (c) plural forms of these terms. For each technical term, the first paragraph of occurrence in the Collected Papers is provided together with its date.

For each one of these terms we computed two measures: the strangeness, measured as the surprisal of a character-level LSTM, and the predicted repetitiveness, measured by means of a Word2vec SGNS.

### Strangeness
A character-level LSTM was trained on a lexicon of standard historical English, namely the unigrams of the [COHA – Corpus of Historical American English](https://www.english-corpora.org/coha/), restricted to the period 1810-1910 and upsampled to weight in their natural frequency. We experimented with several upsampling strategies; the one used in the paper upsamples Q(F) times a word with frequency F, with
```
Q(F) = np.log(F) + F**0.15
```
The [fully trained LSTM](the_good_the_effective_the_ugly/char_lstm_COHA_1810-1910_v2.pt) is here and the code to load and use it is in [this notebook](the_good_the_effective_the_ugly/COHA_LSTM.ipynb). 

The LSTM provides character-level surprisal. To get word-level surprisal, words length has to be token in account, since surprisal of standard English words is (roughly) a function of their length *n*, with *s(n) = a + b/(n^c)*. Below is the plot for the COHA unigram dataset and the interpolant.

<img width="827" height="520" alt="image" src="https://github.com/user-attachments/assets/44b43094-5c1d-472a-9a55-88897661d47d" />

This interpolant can be used to correct mean surprisal computed with our LSTM for any *n*-gram. This way we can turn character-level surprisal to word-level surprisal. The result for Peirce's technical terms is as follows; [click here]() for an interactive version.

<img width="827" height="567" alt="fig_3_2" src="https://github.com/user-attachments/assets/730babb4-a3ee-44b8-a185-9fc0586874ae" />

### Predicted repetitiveness
The chosen measure was the simoid of the dot product between the target embedding and the context embedding in a Skip-Gram Word2vec. See the [paper]() for details.

