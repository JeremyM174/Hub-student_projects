# :book: Automatic fraud detection: the docs

### :bookmark: Table of contents

1. [The tools](#hammer_and_wrench-the-tools)
2. [The files](#books-the-files)
3. [The reasoning](#thought_balloon-the-reasoning)

---

### :hammer_and_wrench: The tools

* Environment manager: Anaconda
* Environment: see the `.yaml` file
* IDE: VScode
* Data warehouse: [Neon](https://neon.com/)
* Data storage: [AWS](https://aws.amazon.com/)

### :books: The files

You may find in this repository's root:

* An instructions file `.env_example.md` to create your confidential environment variables;
* The `afd_project_environment.yaml` file storing the environment's specs to run the notebook;
* The files associated to our containers with the `docker-compose.yaml`, the `Dockerfile` and the `requirements.txt`;
* The `.ipynb` notebook storing the machine learning work;
* An example of data fed by the API with `test_api.json`.

You may also find several folders:

* `dags` which will store the Airflow DAGs and an accompanying script for custom functions;
* `data` which will store the latest extracted data to be fed to our system, as well as the objects produced from machine learning to transform data before checking its fraudulous status;
* `logs` & `plugins` involved in Airflow's running;
* `tmp` which stores temporary data such as the daily report sent by our system.

### :thought_balloon: The reasoning

As this topic will be a much lengthier read, it is covered and translated in both subfolders in these `docs`, depending your preferred language.