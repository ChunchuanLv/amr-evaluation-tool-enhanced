# amr-evaluation

Evaluation metrics to compare AMR graphs based on Smatch (http://amr.isi.edu/evaluation.html). The script computes a set of metrics between AMR graphs in addition to the traditional Smatch code:

* Unlabeled: Smatch score computed on the predicted graphs after (canonicalizing direction and) removing all edge labels 
* No WSD. Smatch score while ignoring Propbank senses (e.g., duck-01 vs duck-02)
* Named Ent. F-score on the named entity recognition (:name roles)
* Non_sense_frames. F-score on Propbank frame identification without sense (e.g. duck-00)
* Frames. F-score on Propbank frame identification without sense (e.g. duck-01)
* Wikification. F-score on the wikification (:wiki roles)
* Negations. F-score on the negation detection (:polarity roles)
* Concepts. F-score on the concept identification task
* Reentrancy. Smatch computed on reentrant edges only
* SRL. Smatch computed on :ARG-i roles only

The different metrics were introduced in the paper below, which also uses them to evaluate several AMR parsers:

"An Incremental Parser for Abstract Meaning Representation", Marco Damonte, Shay B. Cohen and Giorgio Satta. Proceedings of EACL (2017). URL: https://arxiv.org/abs/1608.06111

**(Some of the metrics were recently fixed and updated)**

**Usage:** ```./evaluation.sh <parsed data> <gold data>```,
where <parsed data> and <gold data> are two files which contain multiple AMRs. A blank line is used to separate two AMRs (same format required by Smatch).

In the paper we also discuss a metric for noun phrase analysis. To compute this metric:

- ```./preprocessing.sh <gold data>``` and ```python extract_np.py <gold data>``` to extract the noun phrases from your gold dataset. This will create two files: ```np_sents.txt``` and ```np_graphs.txt```.
- Parse ```np_sents.txt``` with the AMR parser and evaluate with Smatch ```python smatch/smatch.py --pr -f <parsed data> np_graphs.txt``` 
