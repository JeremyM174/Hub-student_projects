# :book: Conversion rate: the docs

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
* The `.csv` source datasets for ML training and testing,
* The `.yaml` file storing the environment's specs to run the notebook.

### :thought_balloon: The reasoning

Although the notebook can be read, here is the summary of its contents:

* **EDA**

Our dataset has 280 000+ lines. At first sight through a sample, we can notice two trends: younger people (below 50 y.o., sorry for those above) seem to be the ones subscribing to the newsletter, and the more pages an user visited, the more likely they are to subscribe.

SEO (Search Engine Optimization) seems to be the most used mean in reaching out to potential subscribers, while these people are found in the USA.

* **ML**

After the removal of nonsensical age values (above 100 y.o.), the casting of binary values to booleans (0/1 for not/new user) and pre-processing, a baseline model (a logistic regression without hyperparameter tuning) is produced and achieves a F1-score of 0.75.

But this project is inspired by a challenge. How about pushing it in an attempt to achieve the best performances we could?

Comes then a multimodel assessment, trying out every classifier model sklearn offers. Selecting the four best models from all these basic trainings, the four competitors are now thrown at Optuna in an attempt to identify the ideal hyperparameters!

The outcome brings out two challengers: the classical Logistic Regression (LR) and the eXtreme Gradient Boosting Classifier (XGBC).  
Pushing again further the hyperparameter tuning, this time these two are thrown into a GridSearch to carefully explore values.  
Thus the champion rises: the XGBC model takes the crown with the best F1-score (0.9855) using weighted averages!

* **Main features**

With all that being done, comes what really answers to the objective set by Data Science Weekly: understanding the levers for customer conversion.

Displaying those with a visualisation, the most noticeable argument towards subscription is (although it could be expected) the seemingly high interest in data science content, as the amount of pages visited works the best for subscription.

The regions the most interested in subscribing seem to be China & USA, while being an user on their website is considered completely irrelevant by our model.

As we deal with a younger audience, age also plays a part; according as well to our model, directly reaching out to potential new subscribers would be the best marketing option.

Thus our bottom line: since visitors seem to react the most to the content provided, we could recommend Data Science Weekly to give an incentive in registering as a user to see what impact it could have, while targeting North American & Chinese markets for a younger audience!