Fraud detection here is based on machine learning, so let's review it!

### Sourcing

Fortunately, given Stripe already existed before the start of this project, past transactional data can be recovered to start training a new algorithm. What it needs however is for said data to be manually checked by partners, to mark which transactions happened to prove fraudulous; these would serve as our target for training!

---

### Training

With a reliable source acquired, training could take place on-premise. The format and content of the data upstream must be identified; for flexibility there could be pipelines feeding the app and model parameters fitting the signal emitted by Stripe, however it would still take more pipelines to make the app output fit the OLTP schema. Instead it would be cheaper and more efficient to ensure consistency between the app input and OLTP input to reduce the amount of necessary work, barring requirements due to regulations compliance.

Of course, EDA & preprocessing steps would take place before literal training. From there, scientists could be free to experiment: feature engineering, algorithm variety, and so on and so forth - an efficient model doesn't have to be complicated, but it takes experimentation to try out hyperparameters and see which models are the most promising!

---

### Storing

Anyhow, the topic of storage remains omnipresent. Past questions of (again) compliance and security, MLflow would be the ideal tool to store all data pertaining to the trained models; behind MLflow would run NeonDB as its backend store and AWS S3 to host artifacts. Without further needs for architecture, MLflow can promote some models as "staging" for a challenger performing well against a "champion" put in production, enabling thus with the proper pipeline the promotion of the challenger into production should it defeat the champion before automating the deployment!

---

### CI/CD

Once live, the source of new data comes from our system. It would take the identification amongst new transactions of which ones really were fraudulous, in order to enrich a training file with new targets that could be ingested by our machine learning. Both the OLAP as well as the noSQL can serve as a source, although it may take transformations to allow it; Jenkins here could be dedicated to these tasks and involve testing throughout the entire process to ensure viability.

Continuous Integration should involve sufficient automation to recognize the promotion of a new model in production, in order to trigger the Continuous Deployment; this way a new model can be pushed to the fraud detection app depending a cron expression, in order to prevent the sudden interruption of service at an inopportune time.

In turn, robust pipelines wouldn't change the behavior of the system; only the content of the "model_version" row would change by including the latest versioning in production, and the "ML_features" collection changing to whatever is included in this new model.

---

### Monitoring

Regardless of performance, a model only captures a static context, it doesn't evolve on its own. As reality evolves, it gradually performs worse with time passing; this is why we want Evidently AI to monitor how our model *lives* beyond a simulated environment.

Evidently makes it possible to track any metric deemed of note to evaluate when does the model start facing data drift, whichever form it takes - data drift ("world is different"), label drift ("outcomes are skewed") or concept drift ("previous patterns changed"). Alerts can then be raised, and a new training triggered by calling back Airflow to ensure competitiveness.

With the proper automation, these reports can also be compiled and stored back into the system everytime they're produced!

---

### Orchestration

Finally, let's remind Airflow oversees the entire process. As much as it can call on Jenkins for the CI/CD part, it could very well handle it on its own; something that comes with its own ups and downs. It does simplify the system and reduces interaction between different components (by literally taking one of them, Jenkins, out of the picture) but will mean a much higher need to secure Airflow.

However one massive advantage in proceeding this way is the ease in recovering the logs & transmitting them. Whether for an audit or because of system errors, tracing anything down by having the same source & format makes the job that much easier to deal with... still, at the cost of keeping it secure.

It all falls down to business decisions!