# :book: Walmart: the docs

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

Although the notebook can be read, here is a summary of its contents:

* **EDA**

The dataset being already small, it also has missing values. With a little manipulation for convenience (lower case for columns and NaN conversion to numpy NaN objects), the first visualisations do not tell us much of a story at first glance - although the CPI (Customer Price Index) seems to follow particular trends, with periods of a higher cost of living meaning (unsurprisingly) fewer sales. Higher temperatures also seem to dissuade customers from shopping.

* **ML**

Cleaning our data a little proves necessary as sometimes, either the weekly sales, either the dates are missing. Since we cannot reasonably infer those, the relevant lines are dropped - which proves to be a heavy hit, with ~30% data lost.

The date column takes some work to make it usable by our machine. While at it, a little feature engineering breaks it down to enlarge the available features in our model, and even includes US holidays flags.

Before preprocessing, another correlation matrix is produced to compare the state before & after the earlier removal of data; the trends do seem similar. The very few outliers in our features are removed, still keeping the data lost around 30%.

Once the preprocessing and training are done, comes fighting overfitting; a lasso regularization with an alpha=1e3 hyperparameter works best. But it would be boring to stop there, so a GridSearch is ran through all three methods of regularization!

In the end, the crowned champion is again the lasso regularization, although on a different alpha (533 as a lengthy decimal) for a R² score of ~0.9669!