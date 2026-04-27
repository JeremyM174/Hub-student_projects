# :book: Kayak: the docs

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

### :books: The files

You may find in this repository's root:

* The `.ipynb` notebook storing all the work for this project, following a logical read and calling external scripts when needed;
* An instructions file `.env_example.md` to create your confidential environment variables;
* The `.yaml` file storing the environment's specs to run the notebook.

You will find under the `src` folder:

* The `booking_url_hotel.py` script gathering 20 relevant hotel URLs for each destination,
* The `booking_info_hotel.py` script scraping each hotel URL to gather the data we need to produce our recommendations.

Finally, the `data` folder stores all `.json` and `.csv` results from the various steps of data collection and transforming.

### :thought_balloon: The reasoning

>WIP