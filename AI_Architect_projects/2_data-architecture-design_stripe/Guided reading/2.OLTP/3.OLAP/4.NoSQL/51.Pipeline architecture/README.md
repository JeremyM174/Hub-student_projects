And now for a focus on our pipelines!

Let's remind what our technical stack is made of:
* Our OLTP is based on PostgreSQL,
* Our OLAP is Amazon's Redshift,
* Our noSQL is mongoDB,
* Our orchestrator is Airflow,
* Data transfer is managed by Airbyte (batches) and Kafka (streaming),
* Fraud detection would be coded into a Streamlit app,
* Machine learning tracking would be enabled by MLflow,
* NeonDB and Amazon's S3 would run behind MLflow's needs,
* CI/CD would be managed by Jenkins,
* Finally monitoring would take place with Evidently AI.

With that being said, what is the idea behind the main flux connecting our elements?

---

### OLTP -> OLAP

The information extracted from the fraud detection app must be transformed by our pipeline to fit our OLTP's schema; please refer to its dedicated document to review it. Since both OLTP & OLAP have strict schemas, the pipeline importing the data to the OLAP becomes an easier task: it begins with an exact import of the OLTP's content, building this way the fact and dimension tables of the OLAP.

Where the pipeline shines though is its ability to further develop on the content provided upstream: by building the OLAP aggregation tables. It becomes thus possible through the pipeline to extract and duplicate information, based on whichever business needs, to produce some frequently requested aggregations such as monthly merchant revenue following this example:

* Extracting the OLTP transaction, merchant & product tables,
* Extracting as well the reference table for dates,
* Transforming their contents to compute basic statistics (sums, averages...) on the expected month,
* Before loading them into an aggregation table of monthly revenue.

To image it, the end result is displayed within the OLAP representation as agg_monthly_merc_revenue; as simple an example as it may be, its possibilities are many. However the strictness of the schemas also imposes its limits: while the pipeline linking both OLTP & OLAP can remain simple, the schemas do not easily answer any and all questions - flexibility that would instead be allowed by the noSQL!

---

### OLAP -> noSQL

As the noSQL component is able to welcome semi-structured or even unstructured data, it is able to escape the strict nature of the OLTP & OLAP to fully adapt to business needs. As we resort to a document-oriented database, the logic behind building its collections no longer is "what constraints do we have to produce an answer?", but rather "what do we want to include in our answer?". The difference may sound subtle, but the freedom in including content is far larger!

The possible pipelines then become limitless, as the question now guides the production of a collection. Let's take a very simple example with machine learning: "how efficient was this given model version at detecting frauds?" The OLTP & OLAP do have part of the answer, with the OLAP able to provide an aggregated table including computations about how many frauds were detected. Now what if you would like to include human interaction, with the manual checking whether the prediction matches reality? You would need the information to be provided at some point - yes, if the pipeline created the row to provide a field even with a placeholder, a simple UPDATE clause could do. What if you wanted to JOIN the information with an audit? This is still possible since we were asked to include those in the OLAP, yet JOINs are known to be expensive - else it would require the creation of a new aggregation table, possibly requiring more resources for our OLAP which only scales vertically. Finally, what if you wanted to include ML features in your answer, should one of them prove to cause trouble? Following our instructions, these are only fed straight to the noSQL, so the OLAP simply cannot include it in its answer.

What is the point then of this lengthy demonstration? Again: the difference between the OLAP's "what constraints do we have to answer?", where ML features cannot be included in the OLAP's answer as opposed to the noSQL's "what do we want to include?". The pipeline's job then may take a lot of customization, but despite no longer having a convenient tabular information it can return *any* content provided upstream, and even enables embedding to make querying simpler. As agile methods are widespread, such behavior fits well its practices. Request example included in the last queries document!

---

### Connections & orchestration

The entirety of the project is orchestrated by Airflow, which makes it possible to organize with precise timing when would each step be triggered. It consequently oversees the connections managed by Airbyte and Kafka, with a simple DAG example being a daily batch: with a cron expression or simply the @daily tag, it could run airbyte_extract_postgres -> transform_for_aggregations -> airbyte_load_redshift.

The convenience brought by Airflow can be found in its webserver (UI): it allows the user to monitor the state of the pipelines, which ones are running, failing, alongside execution statistics and the control over said pipelines. Though it takes some knowledge of Python coding, the content of the DAGs make dependencies manageable and even customizable, and alerts can be raised whenever something goes wrong.

The one thing these tools do not manage is the consistency in the teams' practices. It takes managerial methods to spread cohesive guidelines so the newly developed content can easily integrate itself with the existing framework, rather than requiring further modifications that could break the entire system's logic!