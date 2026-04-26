# :book: AT&T: the docs

### :bookmark: Table of contents

1. [The tools](#hammer_and_wrench-the-tools)
2. [The files](#books-the-files)
3. [The reasoning](#thought_balloon-the-reasoning)

---

### :hammer_and_wrench: The tools

* Environment manager: Anaconda
* Environment: see the `.yaml` file
* IDE: VScode

### :books: The files

You may find in this repository:

* The `.ipynb` notebook which stores the entirety of the work,
* The `.csv` source dataset,
* The `.yaml` file storing the environment's specs to train the model again.

### :thought_balloon: The reasoning

Since the work is all included in the `.ipynb` notebook, the file is meant to be read like a book to progressively explore its steps.

To sum them up: we want first to understand the source dataset, since no details were provided about it. Finding its encoding, we then explore it; the structure is very simple, still not being told what the columns "Unnamed:2/3/4" are exactly is frustrating. Replies? Consecutive messages from the same sender? Character limit? For simplicity, the contents are concatenated - tokenization should still recover the sentiment.

Then the ham/spam label column is remapped to 0 & 1 values (1 being our target, the spam); we notice though how uneven the distribution is, with only 13.41% of spams in our dataset. Past these preparations comes the deep learning with the intent of producing three models: one that serves as a baseline by immediately encoding tokens (with openAI's cl100k), another which will go through lemmatization, and finally a different tokenizer (Google's bert-base-uncased).

For each model, several steps specific to deep learning follow; the conclusions for each one are meant to popularise what it means, making use of confusion matrices.

In the end, an efficient model doesn't have to be complicated; it is the simplest one, the baseline model which performs best! All three however meet the same limitation, which is frequent with NLP: irony. The rare spams making it through our filter succeed thanks to that principle.