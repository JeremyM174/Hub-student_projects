Stripe's data is invaluable, even moreso as it relates to financial transactions. As such, it is paramount to protect it from unauthorized access or use to prevent repercussions beyond repair and legal disputes. Let's dive into matters of security and compliance!

### Security

Data must be encrypted both at rest and in transit. Standards like AES (Advanced Encryption Standard) must be applied to the content of the OLTP, OLAP & noSQL components, while transit should go through TLS (Transport Layer Security) to protect communications between them. Network safety would take an expertise beyond the scope of this project, yet definitely requires consideration. Several services like AWS do provide solutions to that end.

Credentials should only be made available on a need basis, not any other case. Their management can vary depending the situation, although tools like AWS KMS (Key Management Service) can greatly ease the task and reduce risks of a mistaken share, or worse, a leak. Centralizing this way the tokens or API keys also ease tracking who gained access to what; at the same time, the duration of such credentials should rotate regularly to renew the security of the system, in case a leak went unnoticed.

To give an example, analysts should only be able to read the content of the OLAP or noSQL, not write. Scientists should be able to write data pertaining to machine learning (given our cascading system, for safety it could only be writing on the OLAP so the noSQL eventually inherits the new data), but reading would be restricted to the few tables directly involving ML entries (thinking of the variety of aggregated tables or collections including ML). Engineers could write on many levels apart from logs or transactions content, but not read aggregated tables outside a testing environment. Compliance officers could read anytime anywhere, but never write, and so on and so forth; always depending on the role, on the need by providing the least rights.

Given Airflow is expected to orchestrate the entire system, it is an especially important component requiring attention. Although able itself to store and hide credentials, accessing its admin console should be extremely narrowed down, preferably to stakeholders given their legal responsibility.

Depending business decisions, external tools can assist with assessing and managing security, like Splunk or Vormetric.

---

### Compliance

Each region enforces its own regulations, with which the system must comply. To name a few, when pertaining to payments the system should comply with PCI-DSS standards; only few elements pertaining to a transaction should be made use of, while the references like a credit card number should never be readable.

Europe enforces GDPR & its AI Act, implying several restrictions on what machine learning can use while a wealth of personal data, such as the customer's name must be anonymised. A limit in storage duration of the "personal data" must be ensured as well, while the end user should be able to access, rectify or delete their data on their request.

Finally, another example would be the CCPA in the US, allowing customers to opt out of data collection. They should also be able to identify when was their data generated, through which functionality of the related system.

Considering the sheer variety of regulations, external services can help with the tasks involved in this compliance, although at a cost. TrustArc or Verasafe are amongst them, then again their access should be heavily restricted and it could take some effort to produce alerts and/or logs to be recovered by the system presented in this project, so the data can be stored in the OLAP.