# :book: GetAround: the docs

### :bookmark: Table of contents

1. [The tools](#hammer_and_wrench-the-tools)
2. [The files](#books-the-files)
3. [The links](#link-the-links)
4. [The reasoning](#thought_balloon-the-reasoning)

---

### :hammer_and_wrench: The tools

* Environment manager: Anaconda
* Environment: see the `.yaml` file
* IDE: VScode
* Hosting: HuggingFace

### :books: The files

You may find in this repository:

* The `.ipynb` notebook which trained the model,
* The `.joblib` file as our rental cost's prediction model (to be requested through the API `/predict` endpoint),
* The `.yaml` file storing the environment's specs to train the model again,
* The `api` folder used to serve the API documentation & `/predict` endpoint,
* The `streamlit` folder used to deploy the analytical dashboards.

The source datasets are found within the notebook.

### :link: The links

* The analytical [dashboards](https://mevelios-getaround-projectm174.hf.space/) (also includes a tab for price prediction)
* The API [documentation](https://mevelios-getaround-projectn174.hf.space/docs)
* The API [endpoint](https://mevelios-getaround-projectn174.hf.space/predict) (to be pasted as the target of your curl command)

### :thought_balloon: The reasoning

* **EDA with the dashboards:** time delta and contract types

Two dashboards are provided: the first is meant to display the share of each contract type when the vehicle is returned late, while the second dashboard is about the share of contracts being actually cancelled or completed - again when the vehicle is returned late.

Let's focus on the first: based on the provided dataset, what we are interested in are consecutive rentals. Hence a starting filter: by default more than 91% of the rentals are ignored since they either lack the information, either weren't rented again in the next 12 hours.

Here, a convenient slider (the "time delta filter") is enabled to set a minimal and maximal value on this 12-hours span. Depending on how it is used, values are computed to understand how many rentals are included ("rentals kept") or excluded ("impacted rentals" and the value converted in percentage) in the filter; manipulating the minimal value is especially convenient to observe the excluded values depending what minimal delay would our product owner impose between rentals.

Now comes one insight we want to demonstrate here: most of these late returns are on shorter timespans. Nearly a third of the "late cases" are found within 90 minutes, so we could advise our product owner to keep the threshold on lower values.

Another insight would relate to the contract type: although the share of mobile contracts is larger, the difference doesn't seem to be noticeable enough to justify restraining this threshold only to one specific kind of agreement.

  

* **EDA with the dashboards:** late checkout impact

We can now switch to the second dashboard with the consequence from a late return, **when** the information was provided. A second convenient slider is available (the "previous delay filter") to adjust the maximum delay value - especially given more than 90% of these are found under 210 minutes.

What is immediately computed is the amount and percentage these impacted rentals (again, when the information was available) represent over the entire dataset, meaning roughly one rental in twenty-five. The "rentals displayed" will be computed again depending on the value set by the slider.

Reducing this maximum value to 210 tells us a lot: despite the amount of owners impacted by late returns, the canceled rentals represent a rather small value. How valuable this share of cancellations is, we'll leave its consideration to our product owner; the one insight we'll use however to advise them is, again, the fact that most of the impacted rentals are found on the lower threshold values - with roughly 75% of these impacted rentals found below a 90 minutes delay, the threshold likely shouldn't exceed this amount of time.

  

* **Price prediction feature:** the convenient alternative to the API

For ease of access, our dashboards aren't the only available feature; rental cost prediction is also made available.

All relevant parameters can be altered on its interface, making it very straightforward to use following the specs provided in our dataset.

  

* **Machine learning:** the training notebook

The topic covered by this skill block being deployment rather than machine learning, there were no performance requirements to achieve. Managing a R² score of ~0.75 on the first tested algorithm past the hyperparameter tuning seemed satisfying enough for the task at hand.

The notebook also includes a Python HTTP request to test our API. Still, it is advised to resort instead to the handy prediction feature above.

Finally, the notebook ends with a slightly different approach from our dashboards: it is meant to complete the earlier views by distinguishing the contract types amongst the rentals impacted by a late checkout. Our earlier advice about applying the renting delay for all contracts still stands given the cancellations distribution.

  

* **API serving:** documentation and `/predict`

The API is very straightforward and only meets the project's criterias - little to say about it, the accepted parameters are found under the drop-down menu of the predict endpoint.

For user convenience though, making use of the dashboard's interface to switch to cost prediction is handier.