Following our diagrams, let's see a few example queries now:

### SQL (OLTP/OLAP)

* Question: "How much money in their respective currencies transited today through France?"

```
SELECT
    dcu.currency,
    dco.country,
    dd.date,
    SUM(f.transaction_amount) AS total_flux,
    COUNT(*) AS nb_transactions
FROM fact_transactions f
JOIN dim_date dd            ON f.date_time = dd.date_time
JOIN dim_countries dco      ON f.location = dco.location
JOIN dim_currencies dcu     ON f.currency = dcu.currency
WHERE dco.country='France' AND dd.date='2026-02-17' AND f.status='completed'
GROUP BY
    dcu.currency,
    dco.country,
    dd.date
ORDER BY dcu.currency
```

* Question: "What were the last 20 transactions made by the 'cus...x86' customer?"

```
SELECT 
    f.transaction_id,
    f.transaction_amount,
    f.currency,
    dm.company_name,
    dp.name,
    dd.date
FROM fact_transactions f
JOIN dim_merchants dm       ON f.merchant_id = dm.merchant_id
JOIN dim_products dp        ON f.product_id = p.product_id
JOIN dim_date dd            ON f.date_time = dd.date_time
WHERE f.customer_id = 'cus...x86' AND f.status='completed'
ORDER BY dd.date DESC
LIMIT 20;
```

---

### noSQL

Let's develop here an example from the ![pipeline architecture](51-Pipeline_architecture.md) we developed earlier. We'll assume the collection has been extended to include the OLAP's audit logs.

* Question: "What were the characteristics and the audit's results of the production_42 model?"
```db.collection_ML_features.find({"ML_version":"production_42"})```

```
{
    "ML_version" : "production_v42",
    "transaction_ID" : [
        "tra...95d", "tra...b60", "tra...f7t"
    ],
    "ML_features" : {
        "model" : "LogisticRegression",
        "parameters" : {
            "penalty" : "l1",
            "C" : "0.1",
            "random_state" : "42"
        }
    },
    "audit" : {
        "audit_id" : "aud...r6n",
        "audit_log" : [
            ...
        ],
        "date_time" : "2025-03-24 15:57:38.000461"
    }
}
```

Let's give a more striking image of how would we create from scratch a new collection depending on the question, using existing entities from the tables and collections we already covered so far, but assembling them in a completely new way!
* Question: "In the survey 'sur...j21', how well was received the 'pro...2fe' product?"
```df.collection_satisfaction_survey.find({"survey_id" : "sur...j21"}, {"product_id" : "pro...2fe"})```

```
{
    "survey_id" : "sur...j21",      #inherited from noSQL collection_customer_feedback
    "product_id" : "pro...2fe",     #inherited from reference data (product catalogs)
    "name" : "shiny_keyboard",      #reference data (product catalogs)
    "count_messages" : "4096",      #noSQL collection_customer_feedback
    "average_note" : "3.9"          #computed upstream; could've been retrieved with the aggregate() method
}
```