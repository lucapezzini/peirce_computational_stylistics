# Peirce computational stylistics
Some code for an on-going analysis of CS Peirce's works by computational stylistics, performed by Luca Pezzini and Bea Somà. 

## The good, the effective and the ugly
This part of the analysis focuses on the strangeness of Peircean terminology and on the repetition of technical terms. [Here]() is the full paper. Cite as:

```
@article{pezzini_soma_2025_peirce,
author = {Pezzini, Luca and Somà, Beatrice},
title = {The good, the effective and the ugly. Computational insights into the philosophical style of C.S. Peirce},
year = {2025},
addendum = {accepted for publication}
}
```

We extracted a [sample of ~1000 technical terms by CS Peirce](https://github.com/lucapezzini/peirce_computational_stylistics/blob/main/peirce_technical_terms_CP.txt). They are (a) terms of the Collected Papers which occurr as entries in the [Commens Dictionary](http://www.commens.org/dictionary/), (b) technical terms which are italicized in the Collected Papers, automatically extracted and hand-checked to exclude titles, emphasis and foreign words, (c) plural forms of these terms. For each technical term, the first paragraph of occurrence in the Collected Papers is provided together with its date.

Of these terms we computer two measures: the strangeness, measured as the surprisal of a character-level LSTM, and the predicted repetitiveness, measured by means of a Word2vec SGNS.

### Strangeness
The LSTM was trained on a lexicon of standard historical English, namely the unigrams of the [COHA – Corpus of Historical American English](https://www.english-corpora.org/coha/), restricted to the period 1810-1910. 

### Predicted repetitiveness
The chosen measure was the simoid of the dot product between the target embedding and the context embedding in a Skip-Gram Word2vec. 

