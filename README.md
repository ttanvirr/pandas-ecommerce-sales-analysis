# E-commerce Sales Analytics with Python and Pandas

A beginner-friendly, step-by-step learning project using the **Brazilian E-Commerce Public Dataset by Olist**. You will practise Python fundamentals and Pandas together, investigate real business questions, create visualisations, and publish your work on GitHub.

> **How to use this guide:** Follow the numbered steps in order. Attempt each challenge before opening its **Show Solution** section. The solutions are included for checking your work, not for copying before you try.

---

## Table of Contents

- [1. Project Introduction](#1-project-introduction)
- [2. Prerequisites and Environment Setup](#2-prerequisites-and-environment-setup)
- [3. Project Folder and File Creation](#3-project-folder-and-file-creation)
- [4. Dataset Download and Exploration](#4-dataset-download-and-exploration)
- [5. Data Cleaning and Preparation](#5-data-cleaning-and-preparation)
- [6. E-commerce Data Analysis Challenges](#6-e-commerce-data-analysis-challenges)
- [7. Python Fundamentals Practice](#7-python-fundamentals-practice)
- [8. Data Visualization](#8-data-visualization)
- [9. Final Project Organization and GitHub Publication](#9-final-project-organization-and-github-publication)
- [10. Recommended Working Routine](#10-recommended-working-routine)
- [11. Dataset Notes, Definitions, and References](#11-dataset-notes-definitions-and-references)

---

# 1. Project Introduction

## 1.1 What are you building?

You will act as a junior data analyst for an e-commerce business. The business has provided records about orders, customers, products, sellers, payments, delivery, and customer reviews. Your job is to inspect the data, prepare it for analysis, answer business questions, and communicate the findings with charts and written explanations.

The dataset contains approximately 100,000 orders from a Brazilian e-commerce marketplace. It is divided into multiple CSV files rather than one large spreadsheet. This gives you practice with the kind of related data tables you may encounter in a real company.

**Project source:** [Brazilian E-Commerce Public Dataset by Olist on Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

## 1.2 What you will practise

### Python fundamentals

- Variables, strings, numbers, booleans, and `None`.
- Lists, tuples, sets, and dictionaries.
- `if` / `elif` / `else`, `for`, and `while` loops.
- List and dictionary comprehensions.
- Functions, parameters, arguments, and return values.
- Lambda functions.
- Imports, modules, file paths, and exception handling.

### Pandas and data analysis

- Reading CSV files and inspecting DataFrames.
- Selecting, filtering, sorting, and transforming data.
- Finding missing values and duplicate records.
- Converting data types, especially dates.
- Creating calculated columns.
- Grouping and aggregating data.
- Combining related datasets with `merge()`.
- Using `pivot_table()`.
- Checking whether a calculation is at order, item, payment, review, or customer level.

### Communication and project skills

- Turning business questions into analysis tasks.
- Making charts with Matplotlib and Seaborn.
- Writing concise findings supported by evidence.
- Organising a Python project.
- Using Git and GitHub to publish your work.

## 1.3 Questions the project will investigate

By the end, you should be able to answer questions such as:

1. How many orders are in the dataset, and what are their statuses?
2. How do completed-order product sales change month by month?
3. Which product categories have the highest product sales and most line items?
4. Which Brazilian states account for the most orders and distinct customers?
5. How many distinct customers placed more than one delivered order?
6. Which payment methods appear most often, and what is their payment value?
7. How often were delivered orders received after the estimated delivery date?
8. How do average review scores differ between late and on-time/early deliveries?

You may discover that the data cannot answer every business question perfectly. Explain limitations rather than making assumptions.

## 1.4 Final deliverables

Your completed GitHub repository should contain:

- A clearly organised project folder.
- One or more Jupyter notebooks documenting exploration and analysis.
- Reusable Python modules for loading, cleaning, and analysing data.
- Saved charts in `reports/figures/`.
- A final project README describing the dataset, method, analysis, findings, and limitations.
- A `requirements.txt` listing the Python packages needed to run the project.

**Completion standard:** Another person should be able to read your repository, download the dataset from its original source, install the dependencies, and follow your notebook without needing your personal explanation.

---

# 2. Prerequisites and Environment Setup

## 2.1 Required tools

| Tool                                      | Purpose                             | Required?          |
| ----------------------------------------- | ----------------------------------- | ------------------ |
| Python 3.11 or newer                      | Run Python code                     | Yes                |
| `pip`                                     | Install Python packages             | Yes                |
| Visual Studio Code or another code editor | Edit `.py` files and README         | Recommended        |
| Jupyter Notebook                          | Work through analysis interactively | Yes for this guide |
| Git                                       | Track project changes               | Recommended        |
| GitHub account                            | Publish the project                 | Recommended        |
| Kaggle account                            | Download the dataset                | Yes                |

You do not need a GPU, database server, or machine-learning library for this project. The dataset is manageable on an ordinary development computer, although the geolocation file is comparatively large.

## 2.2 Check Python and pip

Open a terminal. Use **PowerShell** on Windows, or your **Ubuntu terminal** when working in WSL.

### Windows PowerShell

```powershell
py --version
py -m pip --version
```

If the `py` launcher is unavailable but `python` works, use:

```powershell
python --version
python -m pip --version
```

### Ubuntu / WSL Ubuntu

```bash
python3 --version
python3 -m pip --version
```

You should see a Python version of 3.11 or newer and a pip version. If Python is missing, install a current Python 3 release from [python.org](https://www.python.org/downloads/) on Windows or use your Ubuntu package manager / Python installation method on WSL.

> **Important:** Keep the Python interpreter and the virtual environment consistent. If you create the environment with one Python installation, activate that environment before installing or running packages.

## 2.3 Create the project directory

Choose a location where you keep programming projects. The commands below create the project in a folder called `practice` under your home directory. Change the parent directory if you prefer another location.

### Ubuntu / WSL Ubuntu

```bash
mkdir -p ~/practice
cd ~/practice
mkdir -p ecommerce-sales-analysis
cd ecommerce-sales-analysis
```

To confirm that you are in the project directory:

### Ubuntu / WSL Ubuntu

```bash
pwd
```

The final path should end in `ecommerce-sales-analysis`.

## 2.4 Create a virtual environment

A **virtual environment** is an isolated Python package environment for this project. It prevents this project's packages from interfering with packages used by other projects.

The environment directory will be named `.venv`.

### Windows PowerShell

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks the activation script, allow scripts for the current PowerShell process only, then activate again:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

This setting applies only to the current PowerShell process. It does not permanently change the machine-wide execution policy.

### Ubuntu / WSL Ubuntu

```bash
python3 -m venv .venv
source .venv/bin/activate
```

When the environment is active, your terminal prompt usually displays `(.venv)`.

To leave the environment later, run:

```bash
deactivate
```

Activate it again whenever you open a new terminal for this project.

## 2.5 Install the required packages

With `.venv` activated, update pip and install the project packages.

### Windows PowerShell and Ubuntu / WSL

The commands are the same in both environments after the virtual environment is activated:

```bash
python -m pip install --upgrade pip
python -m pip install pandas matplotlib seaborn jupyterlab ipykernel
```

Package purposes:

| Package      | Purpose                                                     |
| ------------ | ----------------------------------------------------------- |
| `pandas`     | Read, clean, combine, and analyse tabular data              |
| `matplotlib` | Create charts                                               |
| `seaborn`    | Create statistical visualisations with less styling code    |
| `jupyterlab` | Run the modern JupyterLab interface                         |
| `ipykernel`  | Make this virtual environment available as a Jupyter kernel |

Create or update `requirements.txt` after installation:

```bash
python -m pip freeze > requirements.txt
```

This records the installed package versions so the environment can be recreated later. It may include transitive dependencies as well as the packages you installed directly.

## 2.6 Verify the installation

Run this command while `.venv` is active:

```bash
python -c "import pandas, matplotlib, seaborn; print('pandas:', pandas.__version__); print('matplotlib:', matplotlib.__version__); print('seaborn:', seaborn.__version__)"
```

You should see version numbers and no import error.

## Register the environment as a Jupyter kernel:

```bash
python -m ipykernel install --user --name ecommerce-sales --display-name "Python (ecommerce-sales)"
```

## 2.7 Launch Jupyter Notebook

First, make sure your terminal is in the **project root directory**, `ecommerce-sales-analysis`, and that `.venv` is active.

```bash
jupyter lab
```

Your browser should open the Jupyter file browser.

In Jupyter:

1. Open the `notebooks` folder after you create it in Step 3.
2. Select **New → Python 3** or the kernel named **Python (ecommerce-sales)**.
3. Rename the notebook to `01_data_exploration.ipynb`.
4. Run a test cell:

```python
import pandas as pd

print("Pandas is working:", pd.__version__)
```

If you do not see the `Python (ecommerce-sales)` kernel, refresh the Jupyter page or restart the Notebook server after registering the kernel.

To stop the local Jupyter server, return to its terminal and press `Ctrl + C`. Confirm the shutdown if prompted.

---

# 3. Project Folder and File Creation

## 3.1 Target project structure

Build toward the following structure. You do not need to create every Python file immediately; the guide tells you when to start using each one.

```text
ecommerce-sales-analysis/
│
├── data/
│   ├── raw/
│   │   └── .gitkeep
│   └── processed/
│       └── .gitkeep
│
├── notebooks/
│   └── 01_data_exploration.ipynb
│
├── src/
│   ├── __init__.py
│   ├── data_loader.py
│   ├── cleaning.py
│   └── analysis.py
│
├── reports/
│   └── figures/
│       └── .gitkeep
│
├── .gitignore
├── requirements.txt
└── README.md
```

### What each item is for

| Path                 | Responsibility                                                                        |
| -------------------- | ------------------------------------------------------------------------------------- |
| `data/raw/`          | Original CSV files downloaded from Kaggle. Do not edit these files.                   |
| `data/processed/`    | Optional cleaned or aggregated files that you export during the project.              |
| `notebooks/`         | Jupyter notebooks containing your exploration, challenges, explanations, and results. |
| `src/`               | Reusable Python code that you may import into notebooks.                              |
| `src/__init__.py`    | Marks `src` as a Python package for straightforward imports.                          |
| `src/data_loader.py` | Functions for reading source CSV files.                                               |
| `src/cleaning.py`    | Functions for repeatable cleaning and preparation.                                    |
| `src/analysis.py`    | Functions for repeatable analysis and summary calculations.                           |
| `reports/figures/`   | PNG or SVG charts that you want to show in your report or GitHub README.              |
| `.gitignore`         | Tells Git which local files and folders should not be committed.                      |
| `requirements.txt`   | Lists the Python package dependencies.                                                |
| `README.md`          | Explains how to install, run, and understand the project.                             |

The `.venv/` folder is created by Python and is intentionally not shown in the structure because it should not be committed to Git.

## 3.2 Create the folders and starter files

### Ubuntu / WSL Ubuntu

```bash
mkdir -p data/raw data/processed notebooks src reports/figures
touch data/raw/.gitkeep data/processed/.gitkeep reports/figures/.gitkeep
touch src/__init__.py src/data_loader.py src/cleaning.py src/analysis.py
touch .gitignore requirements.txt
```

The command `touch` creates an empty file if it does not exist. It does not erase an existing file's content.

Create `01_data_exploration.ipynb` from Jupyter rather than making an empty text file. A notebook is a structured JSON document; Jupyter creates the correct format for you.

## 3.3 Add `.gitignore` rules

Open `.gitignore` in your editor and add:

```gitignore
# Python virtual environments
.venv/
venv/

# Python-generated files
__pycache__/
*.py[cod]

# Jupyter-generated files
.ipynb_checkpoints/

# Original and processed datasets
# The source data can be downloaded again from Kaggle.
data/raw/*
!data/raw/.gitkeep

data/processed/*
!data/processed/.gitkeep

# Operating-system files
.DS_Store
Thumbs.db
```

This keeps your downloaded dataset, virtual environment, and generated cache files out of Git. The `.gitkeep` files allow Git to preserve otherwise-empty directories.

Charts in `reports/figures/` are **not ignored**, because selected visualisations are useful project outputs that you may want to publish.

## 3.4 Add package names to `requirements.txt`

Open `requirements.txt` and add these package names, one per line:

```text
pandas
matplotlib
seaborn
jupyterlab
ipykernel
```

If you already ran `python -m pip freeze > requirements.txt`, that command created a version-pinned list. Either a curated list or a frozen list is acceptable for this learning project. Do not manually combine the two formats without checking for duplicate entries.

To install dependencies later on another machine, activate a new virtual environment and run:

```bash
python -m pip install -r requirements.txt
```

## 3.5 Initialise Git

Check whether Git is installed:

```bash
git --version
```

If it is installed, configure your name and email if you have not done so before. Use the name and email associated with your GitHub commits:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Create an **empty** repository on GitHub. Do not initialise it with a README, `.gitignore`, or licence because you will push the files from this local project.

Then, from the project root, run:

```bash
git init
git add README.md .gitignore requirements.txt src
git commit -m "Initialize e-commerce analytics project"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/ecommerce-sales-analysis.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username. If you chose a different repository name, use that exact name in the remote URL.

You may not have all the listed files populated yet. That is fine: this first commit establishes the repository. Add the notebooks, charts, and reusable code in later commits as you complete the project.

---

# 4. Dataset Download and Exploration

## 4.1 Download the dataset

Use the original Kaggle page:

**[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)**

1. Sign in to Kaggle or create a free account.
2. Open the dataset page.
3. Select **Download**.
4. Save the downloaded ZIP archive.
5. Extract its CSV files into your project's `data/raw/` directory.

Do not rename the original CSV files. The exercises use their original names.

### Extract on Windows PowerShell

Replace the example ZIP path with the actual path and filename on your computer:

```powershell
Expand-Archive -Path "$HOME\Downloads\archive.zip" -DestinationPath ".\data\raw" -Force
```

### Extract on Ubuntu / WSL Ubuntu

If the archive is in your Ubuntu Downloads directory:

```bash
unzip ~/Downloads/archive.zip -d data/raw
```

If `unzip` is not installed, install it with your Ubuntu package manager, then run the extraction command again.

## 4.2 Expected CSV files

The public dataset contains these nine files:

| CSV file                                | What one row represents                      | Main use                                         |
| --------------------------------------- | -------------------------------------------- | ------------------------------------------------ |
| `olist_orders_dataset.csv`              | One order                                    | Order status and purchase/delivery dates         |
| `olist_customers_dataset.csv`           | One customer record associated with an order | Customer identity and delivery location          |
| `olist_order_items_dataset.csv`         | One item line within an order                | Product price, freight, seller, and product sold |
| `olist_order_payments_dataset.csv`      | One payment record                           | Payment type, instalments, and payment value     |
| `olist_order_reviews_dataset.csv`       | One review record                            | Review score and review comments/dates           |
| `olist_products_dataset.csv`            | One product                                  | Product category and physical attributes         |
| `olist_sellers_dataset.csv`             | One seller                                   | Seller location                                  |
| `olist_geolocation_dataset.csv`         | One coordinate record for a ZIP-code prefix  | Geographic coordinates                           |
| `product_category_name_translation.csv` | One category translation                     | Portuguese-to-English category names             |

The first three files to use are:

1. `olist_orders_dataset.csv`
2. `olist_order_items_dataset.csv`
3. `olist_customers_dataset.csv`

They let you learn the central relationships: an order has a customer, and an order can contain one or more item lines. Add the other files only when a later challenge needs them.

## 4.3 Important columns and relationships

These are the original column names in the Olist CSV files. The spelling `lenght` in two product column names is a typo in the source dataset; do not silently change the names when reading the CSV.

### Orders — `olist_orders_dataset.csv`

| Column                          | Meaning                                                       |
| ------------------------------- | ------------------------------------------------------------- |
| `order_id`                      | Unique order identifier                                       |
| `customer_id`                   | Identifier for the customer record associated with this order |
| `order_status`                  | Current status recorded for the order                         |
| `order_purchase_timestamp`      | Time the customer placed the order                            |
| `order_approved_at`             | Time the order was approved                                   |
| `order_delivered_carrier_date`  | Time the order was handed to the carrier                      |
| `order_delivered_customer_date` | Time the customer received the order                          |
| `order_estimated_delivery_date` | Estimated delivery date                                       |

### Customers — `olist_customers_dataset.csv`

| Column                     | Meaning                                          |
| -------------------------- | ------------------------------------------------ |
| `customer_id`              | Customer-record identifier linked to an order    |
| `customer_unique_id`       | Identifier for the actual customer across orders |
| `customer_zip_code_prefix` | Customer ZIP-code prefix                         |
| `customer_city`            | Customer city                                    |
| `customer_state`           | Brazilian state abbreviation                     |

**Important customer distinction:** `customer_id` is associated with an individual order record. A repeat buyer can have different `customer_id` values in different orders. Use `customer_unique_id` when counting distinct people or repeat customers.

### Order items — `olist_order_items_dataset.csv`

| Column                | Meaning                                                   |
| --------------------- | --------------------------------------------------------- |
| `order_id`            | Order identifier                                          |
| `order_item_id`       | Item sequence number within the order                     |
| `product_id`          | Product identifier                                        |
| `seller_id`           | Seller identifier                                         |
| `shipping_limit_date` | Deadline for the seller to hand the item to the carrier   |
| `price`               | Product price for this item line, in Brazilian real (BRL) |
| `freight_value`       | Freight amount for this item line, in BRL                 |

There is no separate quantity column in this dataset. Treat each row as one order-item line when counting item lines. Do not claim that the dataset gives the physical unit quantity of every product.

### Payments — `olist_order_payments_dataset.csv`

| Column                 | Meaning                                       |
| ---------------------- | --------------------------------------------- |
| `order_id`             | Order identifier                              |
| `payment_sequential`   | Sequence number for a payment within an order |
| `payment_type`         | Payment method                                |
| `payment_installments` | Number of instalments                         |
| `payment_value`        | Value of this payment record, in BRL          |

An order can have multiple payment rows. Group payments by `order_id` before joining payment totals to a one-row-per-order table.

### Reviews — `olist_order_reviews_dataset.csv`

| Column                    | Meaning                                   |
| ------------------------- | ----------------------------------------- |
| `review_id`               | Review identifier supplied by the dataset |
| `order_id`                | Order identifier                          |
| `review_score`            | Score from 1 to 5                         |
| `review_comment_title`    | Review title; often missing               |
| `review_comment_message`  | Review text; often missing                |
| `review_creation_date`    | Date the review was created               |
| `review_answer_timestamp` | Time the review was answered              |

Not every order has a review, and an order may be associated with more than one review row. Aggregate reviews by `order_id` before joining review metrics to an order-level table.

### Products — `olist_products_dataset.csv`

Columns: `product_id`, `product_category_name`, `product_name_lenght`, `product_description_lenght`, `product_photos_qty`, `product_weight_g`, `product_length_cm`, `product_height_cm`, and `product_width_cm`.

### Sellers — `olist_sellers_dataset.csv`

Columns: `seller_id`, `seller_zip_code_prefix`, `seller_city`, and `seller_state`.

### Geolocation — `olist_geolocation_dataset.csv`

Columns: `geolocation_zip_code_prefix`, `geolocation_lat`, `geolocation_lng`, `geolocation_city`, and `geolocation_state`.

A ZIP prefix can have many coordinate rows. Do not directly join the raw geolocation table to customers or sellers and assume it is one-to-one. Aggregate it to one row per ZIP prefix first if you later need it.

### Category translation — `product_category_name_translation.csv`

Columns: `product_category_name` and `product_category_name_english`.

Use `product_category_name` to connect it to the products table. Some product categories may not have an English translation; preserve those categories with a fallback label instead of dropping them.

## 4.4 Understand the table relationships before merging

The main relationships are:

```text
orders
  ├── customer_id ─────────────── customers
  ├── order_id ────────────────── order_items
  │                                  ├── product_id ── products
  │                                  │                   └── product_category_name ── category translation
  │                                  └── seller_id ─── sellers
  ├── order_id ────────────────── order_payments
  └── order_id ────────────────── order_reviews
```

The central keys are:

| Left table    | Key                     | Right table          | Key                     |
| ------------- | ----------------------- | -------------------- | ----------------------- |
| `orders`      | `customer_id`           | `customers`          | `customer_id`           |
| `orders`      | `order_id`              | `order_items`        | `order_id`              |
| `orders`      | `order_id`              | `order_payments`     | `order_id`              |
| `orders`      | `order_id`              | `order_reviews`      | `order_id`              |
| `order_items` | `product_id`            | `products`           | `product_id`            |
| `order_items` | `seller_id`             | `sellers`            | `seller_id`             |
| `products`    | `product_category_name` | category translation | `product_category_name` |

## 4.5 Challenge 1 — Load the three starting CSV files

1. **Objective:** Read the orders, order items, and customers CSV files into three Pandas DataFrames.
2. **Dataset:** `olist_orders_dataset.csv`, `olist_order_items_dataset.csv`, and `olist_customers_dataset.csv`.
3. **Relevant columns:** No specific columns are required yet. You will inspect them in the next challenge.
4. **Instructions:**
    1. Import `Path` from `pathlib` and `pandas` as `pd`.
    2. Create a path pointing to `data/raw/` from the project root.
    3. Check that all three required CSV files exist.
    4. Load each CSV into a clearly named DataFrame: `orders`, `order_items`, and `customers`.
    5. Print a confirmation after loading.
5. **Expected result:** Three DataFrames exist without a `FileNotFoundError`. Their variable names should match the names above.
6. **Hints:** `Path.cwd()` returns the current working directory. Use `/` to combine `Path` objects with folder or file names. Use `Path.exists()` to check a file.
7. **Skills practised:** Imports, variables, `pathlib`, lists, loops, file paths, `pd.read_csv()`.

<details>
<summary>Show Solution</summary>

```python
from pathlib import Path
import pandas as pd

project_root = Path.cwd()
data_dir = project_root / "data" / "raw"

required_files = [
    "olist_orders_dataset.csv",
    "olist_order_items_dataset.csv",
    "olist_customers_dataset.csv",
]

missing_files = [
    filename
    for filename in required_files
    if not (data_dir / filename).exists()
]

if missing_files:
    raise FileNotFoundError(
        f"Missing files in {data_dir}: {missing_files}. "
        "Download and extract the Olist dataset into data/raw/."
    )

orders = pd.read_csv(data_dir / "olist_orders_dataset.csv")
order_items = pd.read_csv(data_dir / "olist_order_items_dataset.csv")
customers = pd.read_csv(data_dir / "olist_customers_dataset.csv")

print("The three starting datasets were loaded successfully.")
```

**Why this works:** `Path` builds file paths in a way that works across Windows and Linux. The list comprehension checks every required file before Pandas attempts to read it. If a file is missing, the error tells you which file and directory to check.

**If the path check fails:** Make sure you launched Jupyter from the project root, not from inside another folder. You can inspect the current directory with `Path.cwd()`.

</details>

## 4.6 Challenge 2 — Inspect the three DataFrames

1. **Objective:** Understand the size, columns, data types, and basic contents of each starting dataset.
2. **Dataset:** `orders`, `order_items`, and `customers` from Challenge 1.
3. **Relevant columns:** All columns in each DataFrame.
4. **Instructions:**
    1. Print the `.shape` of each DataFrame.
    2. Print the column names as a Python list.
    3. Run `.info()` on each DataFrame.
    4. Display the first five rows of each.
    5. Run `.describe()` on the numeric columns of `order_items`.
    6. Write two or three Markdown observations about what you notice. Do not guess why a value is missing yet.
5. **Expected result:** You can explain how many rows and columns each DataFrame contains, identify its important columns, and recognise which columns are numeric or text-like.
6. **Hints:** `.info()` prints a report and returns `None`; call it on its own line. `describe(include="all")` can include non-numeric columns, but its output is wider.
7. **Skills practised:** Attribute access, method calls, loops, DataFrame inspection, reading output.

<details>
<summary>Show Solution</summary>

```python
starting_datasets = {
    "orders": orders,
    "order_items": order_items,
    "customers": customers,
}

for dataset_name, dataframe in starting_datasets.items():
    print(f"\n--- {dataset_name} ---")
    print("Shape:", dataframe.shape)
    print("Columns:", dataframe.columns.to_list())
    dataframe.info()
    display(dataframe.head())

print("\n--- Numeric summary: order_items ---")
display(order_items.describe())
```

**How to read the result:** A DataFrame's shape is `(number_of_rows, number_of_columns)`. The `info()` report shows non-null counts and data types. The first five rows help you recognise the meaning and format of values.

</details>

---

# 5. Data Cleaning and Preparation

Do not change the original DataFrames unnecessarily. A useful beginner habit is to keep the raw data in its original form and create a new DataFrame when you prepare or transform it. That lets you compare the prepared data with the source.

## 5.1 Cleaning principles for this dataset

- Missing delivery dates are expected for orders that have not reached the customer. Do not fill those dates with invented values.
- Missing product attributes do not automatically make a product record useless. Keep the row and decide whether the missing field matters to your particular analysis.
- Review comments are often missing. A row can still be useful because it may contain a `review_score`.
- Check duplicates using the correct key or combination of columns. Do not automatically delete rows just because one identifier appears more than once.
- Use `errors="coerce"` when converting values if you want invalid values to become missing values that you can inspect. Do not silently discard them.
- Keep a note of every cleaning decision so a reader can understand what you changed and why.

## 5.2 Challenge 3 — Audit missing values and duplicate keys

1. **Objective:** Identify missing values and check whether the expected identifiers are duplicated.
2. **Dataset:** `orders`, `order_items`, and `customers`.
3. **Relevant columns:** `order_id`, `customer_id`, and `order_item_id`.
4. **Instructions:**
    1. Count missing values in every column of each DataFrame.
    2. Check whether `orders.order_id` is duplicated.
    3. Check whether `customers.customer_id` is duplicated.
    4. Check whether the combination of `order_id` and `order_item_id` is duplicated in `order_items`.
    5. Display the rows that fail any of these uniqueness checks.
    6. Do not delete rows yet. Write down what you found.
5. **Expected result:** You have a missing-value count for each table and a duplicate count for each expected key. The order-item key must be checked as a pair, not by `order_id` alone, because one order can contain multiple item lines.
6. **Hints:** Use `.isna().sum()`, `.duplicated()`, and `.duplicated(subset=[...])`.
7. **Skills practised:** Dictionaries, loops, Boolean conditions, missing-value checks, duplicate checks.

<details>
<summary>Show Solution</summary>

```python
for name, dataframe in {
    "orders": orders,
    "order_items": order_items,
    "customers": customers,
}.items():
    print(f"\nMissing values in {name}:")
    display(dataframe.isna().sum().sort_values(ascending=False))

orders_duplicate_mask = orders.duplicated(subset=["order_id"], keep=False)
customers_duplicate_mask = customers.duplicated(subset=["customer_id"], keep=False)
items_duplicate_mask = order_items.duplicated(
    subset=["order_id", "order_item_id"],
    keep=False,
)

print("Duplicate order_id rows:", int(orders_duplicate_mask.sum()))
print("Duplicate customer_id rows:", int(customers_duplicate_mask.sum()))
print("Duplicate order_id + order_item_id rows:", int(items_duplicate_mask.sum()))

display(orders.loc[orders_duplicate_mask].head())
display(customers.loc[customers_duplicate_mask].head())
display(order_items.loc[items_duplicate_mask].head())
```

**Important:** `order_id` is expected to repeat in `order_items` because an order can have several item lines. That is why the combination of `order_id` and `order_item_id` is the relevant check. Missing values in delivery date columns also have a business meaning; do not fill them with the mean or median.

</details>

## 5.3 Challenge 4 — Convert date columns to datetime

1. **Objective:** Convert date/time columns from text into Pandas datetime values so you can calculate durations and group by month.
2. **Dataset:** `orders` and `order_items`.
3. **Relevant columns:**
    - Orders: `order_purchase_timestamp`, `order_approved_at`, `order_delivered_carrier_date`, `order_delivered_customer_date`, `order_estimated_delivery_date`.
    - Items: `shipping_limit_date`.
4. **Instructions:**
    1. Create copies named `orders_clean` and `order_items_clean`.
    2. Convert the listed columns using `pd.to_datetime()`.
    3. Use `errors="coerce"` so an invalid date string becomes `NaT` rather than stopping the whole operation.
    4. Print the data types of the converted columns.
    5. Count the resulting missing datetime values.
    6. Explain why a missing delivered date should not automatically be treated as a data-entry error.
5. **Expected result:** The converted columns have a datetime dtype. Any missing or invalid values are represented as `NaT` and remain visible for inspection.
6. **Hints:** `NaT` is Pandas' missing-value marker for datetime-like data. Use `.isna().sum()` to count it.
7. **Skills practised:** Copying DataFrames, lists, loops, function calls, date conversion, missing-value inspection.

<details>
<summary>Show Solution</summary>

```python
orders_clean = orders.copy()
order_items_clean = order_items.copy()

order_date_columns = [
    "order_purchase_timestamp",
    "order_approved_at",
    "order_delivered_carrier_date",
    "order_delivered_customer_date",
    "order_estimated_delivery_date",
]

for column in order_date_columns:
    orders_clean[column] = pd.to_datetime(
        orders_clean[column],
        errors="coerce",
    )

order_items_clean["shipping_limit_date"] = pd.to_datetime(
    order_items_clean["shipping_limit_date"],
    errors="coerce",
)

print(orders_clean[order_date_columns].dtypes)
print("\nMissing converted order dates:")
display(orders_clean[order_date_columns].isna().sum())

print("\nMissing shipping limit dates:")
print(order_items_clean["shipping_limit_date"].isna().sum())
```

**Why `errors="coerce"` is useful:** It makes problematic values visible as `NaT`. It does not decide whether a missing value is acceptable. You still need to investigate the reason and the business meaning.

</details>

## 5.4 Challenge 5 — Validate prices and create item-level totals

1. **Objective:** Check the numeric price columns and calculate a total amount for each item line.
2. **Dataset:** `olist_order_items_dataset.csv` / `order_items`.
3. **Relevant columns:** `price`, `freight_value`, `order_id`, `order_item_id`.
4. **Instructions:**
    1. Create a copy called `items_clean` from `order_items_clean`.
    2. Convert `price` and `freight_value` to numeric values using `pd.to_numeric(errors="coerce")`.
    3. Count values that became missing.
    4. Create `item_total_brl` by adding `price` and `freight_value` for each item line.
    5. Inspect the smallest and largest values and display rows where either input is missing or negative.
    6. Do not remove those rows automatically. Record the number of suspicious rows and decide whether they affect your later analysis.
5. **Expected result:** `items_clean` has numeric `price` and `freight_value` columns and a calculated `item_total_brl` column. You can inspect suspicious rows rather than hiding them.
6. **Hints:** `.lt(0)` checks whether values are less than zero. Combine Boolean masks with `|` for OR.
7. **Skills practised:** Copies, numeric conversion, arithmetic, Boolean masks, filtering, calculated columns.

<details>
<summary>Show Solution</summary>

```python
items_clean = order_items_clean.copy()

for column in ["price", "freight_value"]:
    items_clean[column] = pd.to_numeric(
        items_clean[column],
        errors="coerce",
    )

print("Missing or invalid price:", items_clean["price"].isna().sum())
print("Missing or invalid freight:", items_clean["freight_value"].isna().sum())

items_clean["item_total_brl"] = (
    items_clean["price"] + items_clean["freight_value"]
)

suspicious_mask = (
    items_clean["price"].isna()
    | items_clean["freight_value"].isna()
    | items_clean["price"].lt(0)
    | items_clean["freight_value"].lt(0)
)

print("Suspicious item rows:", int(suspicious_mask.sum()))
display(items_clean.loc[suspicious_mask].head(20))
display(items_clean[["price", "freight_value", "item_total_brl"]].describe())
```

`item_total_brl` is the product price plus freight for one item line. It is useful as an item-level amount, but keep product price and freight in separate columns too. Do not call this a profit measure: the dataset does not provide all costs needed to calculate profit.

</details>

---

# 6. E-commerce Data Analysis Challenges

Before beginning this section, understand **data grain**. Grain means what one row represents. In this dataset, one row can represent an order, an item line, a payment, a review, or a customer record. A calculation is only meaningful when you know its grain.

## 6.1 A rule that prevents incorrect totals

Do not directly merge `order_items`, `order_payments`, and `order_reviews` together on `order_id` and then sum their values. Each can contain multiple rows for the same order. Joining several one-to-many tables can multiply rows and inflate sums.

A safer approach is:

1. Aggregate each one-to-many table to one row per `order_id` when you need order-level metrics.
2. Merge those aggregated results into an order-level table.
3. Use Pandas merge validation such as `validate="one_to_one"` or `validate="many_to_one"` to check the relationship you expect.

## 6.2 Challenge 6 — Summarise order statuses and order-item values

1. **Objective:** Understand the order-status distribution and calculate product price totals at order level.
2. **Dataset:** `orders_clean` and `items_clean`.
3. **Relevant columns:** `orders_clean.order_id`, `orders_clean.order_status`, `items_clean.order_id`, `items_clean.price`, `items_clean.freight_value`.
4. **Instructions:**
    1. Count orders by `order_status` and sort the result from largest to smallest.
    2. Group item lines by `order_id`.
        1. For each order, calculate the sum of `price`, the sum of `freight_value`, and the number of item lines.
        2. Name the aggregated columns `product_sales_brl`, `freight_brl`, and `item_line_count`.
    3. Merge the order-level item summary with `orders_clean` using `order_id`.
    4. Compare the number of rows before and after the merge.
5. **Expected result:** A status-count Series and an order-level DataFrame with one row per order that has item lines. The row count should not multiply during the merge.
6. **Hints:** Use `value_counts()` for the first task. Use `groupby().agg()` for the second. The item summary has one row per order after grouping.
7. **Skills practised:** `value_counts()`, `groupby()`, `agg()`, `merge()`, `nunique()`, and merge validation.

<details>
<summary>Show Solution</summary>

```python
order_status_counts = orders_clean["order_status"].value_counts()
display(order_status_counts)

order_item_summary = (
    items_clean
    .groupby("order_id")
    .agg(
        product_sales_brl=("price", "sum"),
        freight_brl=("freight_value", "sum"),
        item_line_count=("order_item_id", "count"),
    )
    .reset_index()
)

orders_with_item_summary = orders_clean.merge(
    order_item_summary,
    on="order_id",
    how="left",
    validate="one_to_one",
)

print("Orders before merge:", len(orders_clean))
print("Rows after merge:", len(orders_with_item_summary))
display(orders_with_item_summary.head())
```

The aggregated item table contains at most one row per `order_id`, so a one-to-one merge is appropriate when the orders table also has one row per order. A left join keeps orders even if they have no matching item summary.

</details>

## 6.3 Challenge 7 — Analyse monthly completed-order sales

1. **Objective:** Find how product sales and freight amounts change from month to month for delivered orders.
2. **Dataset:** `orders_clean` and `items_clean`.
3. **Relevant columns:** `order_id`, `order_status`, `order_purchase_timestamp`, `price`, `freight_value`, and `order_item_id`.
4. **Instructions:**
    1. Select only orders whose `order_status` is `delivered`.
        - Keep `order_id` and `order_purchase_timestamp` from the orders DataFrame.
    2. Merge those rows with `items_clean` on `order_id`.
    3. Create a `purchase_month` column from `order_purchase_timestamp` using monthly periods.
    4. Group by month and calculate product price total, freight total, combined item-plus-freight total, distinct order count, and item-line count.
        - Sort the result chronologically.
    5. Identify the month with the highest product price total. Do not invent an explanation for why it was highest.
5. **Expected result:** A month-indexed summary with one row per month in the dataset's period. It should include separate product and freight totals, plus order and item-line counts.
6. **Hints:** Use `.dt.to_period("M")` after converting the date column. Use `nunique` for distinct orders. Use a `many_to_one` validation because many item rows can match one order row.
7. **Skills practised:** Filtering, selecting, merging, date accessors, `groupby()`, `agg()`, sorting, and business metric definitions.

<details>
<summary>Show Solution</summary>

```python
delivered_order_dates = orders_clean.loc[
    orders_clean["order_status"] == "delivered",
    ["order_id", "order_purchase_timestamp"],
].copy()

completed_items = items_clean.merge(
    delivered_order_dates,
    on="order_id",
    how="inner",
    validate="many_to_one",
)

completed_items["purchase_month"] = (
    completed_items["order_purchase_timestamp"].dt.to_period("M")
)

monthly_sales = (
    completed_items
    .groupby("purchase_month")
    .agg(
        product_sales_brl=("price", "sum"),
        freight_brl=("freight_value", "sum"),
        item_and_freight_brl=("item_total_brl", "sum"),
        order_count=("order_id", "nunique"),
        item_line_count=("order_item_id", "count"),
    )
    .sort_index()
)

display(monthly_sales)
print("Month with the highest product sales:", monthly_sales["product_sales_brl"].idxmax())
```

**Metric definition:** This challenge uses the sum of `price` from order-item rows as product sales for delivered orders. Freight is shown separately. The combined column adds product price and freight. These figures are not profit, and they should not be confused with the `payment_value` total from the separate payments table.

</details>

## 6.4 Challenge 8 — Find the strongest product categories

1. **Objective:** Compare product categories using product sales and item-line counts.
2. **Dataset:** `items_clean`, `olist_products_dataset.csv`, and `product_category_name_translation.csv`.
    - **Scope:** This challenge uses all available item lines, regardless of order status. Label the result as an all-status item-line summary; do not compare it directly with the delivered-order-only monthly sales in Challenge 7.
3. **Relevant columns:** `product_id`, `price`, `order_item_id`, `product_category_name`, and `product_category_name_english`.
4. **Instructions:**
    1. Load the products and category-translation CSV files.
    2. Merge `items_clean` with products using `product_id`.
    3. Merge the result with the translation table using `product_category_name`.
    4. Use the English category name when available. If it is missing, keep the original Portuguese category name. If both are missing, use `Uncategorized`.
    5. Group by the resulting category label.
    6. Calculate product sales (`price` sum), item-line count, and distinct product count.
    7. Sort by product sales in descending order and display the top ten categories.
5. **Expected result:** A category summary that keeps untranslated or missing categories rather than dropping them. The top ten are sorted by product sales.
6. **Hints:** Use left joins so products are not removed when a category translation is unavailable. Use `fillna()` in a deliberate sequence. Validate each product/category join as many-to-one.
7. **Skills practised:** Reading additional CSVs, sequential merges, `fillna()`, `groupby()`, `agg()`, sorting, and distinct counts.

<details>
<summary>Show Solution</summary>++

```python
products = pd.read_csv(data_dir / "olist_products_dataset.csv")
category_translation = pd.read_csv(
    data_dir / "product_category_name_translation.csv"
)

items_with_products = items_clean.merge(
    products,
    on="product_id",
    how="left",
    validate="many_to_one",
)

items_with_categories = items_with_products.merge(
    category_translation,
    on="product_category_name",
    how="left",
    validate="many_to_one",
)

items_with_categories["category_name"] = (
    items_with_categories["product_category_name_english"]
    .fillna(items_with_categories["product_category_name"])
    .fillna("Uncategorized")
)

category_summary = (
    items_with_categories
    .groupby("category_name")
    .agg(
        product_sales_brl=("price", "sum"),
        item_line_count=("order_item_id", "count"),
        distinct_products=("product_id", "nunique"),
    )
    .sort_values("product_sales_brl", ascending=False)
)

display(category_summary.head(10))
```

The product table has a few source column names with the spelling `lenght`. You do not need those columns for this analysis. The category translation is a lookup table, so the left join preserves product rows that have no English translation.

</details>

## 6.5 Challenge 9 — Compare orders and customers by state

1. **Objective:** Find which Brazilian states have the most delivered orders and distinct customers.
2. **Dataset:** `orders_clean` and `customers`.
3. **Relevant columns:** `order_id`, `customer_id`, `order_status`, `customer_unique_id`, and `customer_state`.
4. **Instructions:**
    1. Select delivered orders.
    2. Merge them with the customer table using `customer_id`.
    3. Group by `customer_state`.
    4. Calculate distinct order count and distinct `customer_unique_id` count for each state.
    5. Sort by order count from largest to smallest.
    6. Explain the difference between an order count and a distinct customer count.
5. **Expected result:** One row per state with two separate counts. A customer who placed multiple delivered orders contributes more than one to the order count but only one to the distinct customer count.
6. **Hints:** The orders and customers tables should match one-to-one using `customer_id`. Use `nunique()` for both counts.
7. **Skills practised:** Filtering, merging, grouping, aggregation, and understanding customer identifiers.

<details>
<summary>Show Solution</summary>

```python
delivered_orders = orders_clean.loc[
    orders_clean["order_status"] == "delivered"
].copy()

delivered_with_customers = delivered_orders.merge(
    customers[
        [
            "customer_id",
            "customer_unique_id",
            "customer_state",
        ]
    ],
    on="customer_id",
    how="left",
    validate="many_to_one",
)

state_summary = (
    delivered_with_customers
    .groupby("customer_state")
    .agg(
        delivered_orders=("order_id", "nunique"),
        distinct_customers=("customer_unique_id", "nunique"),
    )
    .sort_values("delivered_orders", ascending=False)
)

display(state_summary)
```

The `customer_id` identifies the customer record used by the order. The `customer_unique_id` is the field you need when counting the same real customer across multiple orders.

</details>

## 6.6 Challenge 10 — Identify repeat customers

1. **Objective:** Calculate how many distinct customers placed more than one delivered order.
2. **Dataset:** `orders_clean` and `customers`.
3. **Relevant columns:** `order_id`, `order_status`, `customer_id`, and `customer_unique_id`.
4. **Instructions:**
    1. Merge orders with the two customer identifier columns using `customer_id`.
    2. Filter to delivered orders.
    3. Group by `customer_unique_id` and count distinct `order_id` values.
    4. Create a Series containing customers with more than one delivered order.
    5. Calculate the total number of distinct customers in the delivered-order data, the number of repeat customers, and the repeat-customer percentage.
    6. State clearly that this is a repeat-customer calculation for delivered orders only.
5. **Expected result:** A customer-level order-count Series and a repeat-customer count and percentage. The percentage should use distinct customers as its denominator.
6. **Hints:** A Boolean condition such as `order_counts > 1` can filter the Series. Use `.nunique()` or the length of the grouped Series for the customer denominator.
7. **Skills practised:** Merging, grouping, `nunique()`, filtering a Series, arithmetic, and interpreting identifiers.

<details>
<summary>Show Solution</summary>

```python
orders_with_customer_identity = orders_clean.merge(
    customers[["customer_id", "customer_unique_id"]],
    on="customer_id",
    how="left",
    validate="many_to_one",
)

delivered_customer_orders = orders_with_customer_identity.loc[
    orders_with_customer_identity["order_status"] == "delivered"
].copy()

order_counts_by_customer = (
    delivered_customer_orders
    .groupby("customer_unique_id")["order_id"]
    .nunique()
)

repeat_customer_order_counts = order_counts_by_customer.loc[
    order_counts_by_customer > 1
]

total_customers = int(order_counts_by_customer.size)
repeat_customers = int(repeat_customer_order_counts.size)
repeat_customer_percentage = (
    repeat_customers / total_customers * 100
    if total_customers
    else 0
)

print("Distinct delivered-order customers:", total_customers)
print("Repeat customers:", repeat_customers)
print(f"Repeat-customer percentage: {repeat_customer_percentage:.2f}%")
```

A repeat customer here means a `customer_unique_id` associated with more than one delivered `order_id`. This definition is explicit and reproducible. If you later analyse all order statuses, label that metric differently.

</details>

## 6.7 Challenge 11 — Analyse payment methods without double-counting orders

1. **Objective:** Compare payment methods and calculate total payment value per order without creating duplicate order totals.
2. **Dataset:** `olist_order_payments_dataset.csv` and `orders_clean`.
3. **Relevant columns:** `order_id`, `payment_sequential`, `payment_type`, `payment_installments`, and `payment_value`.
4. **Instructions:**
    1. Load the payments CSV.
    2. Group by `payment_type` and calculate payment-record count, distinct order count, and total payment value.
    3. Sort by total payment value.
    4. Separately group the payment table by `order_id` and calculate total payment value and payment-record count per order.
    5. Merge this one-row-per-order payment summary with the orders table.
    6. Explain why `payment_type` counts can overlap: an order can use more than one payment record or method.
5. **Expected result:** A payment-method summary and a separate order-level payment summary. The latter should have no more than one row per order.
6. **Hints:** A payment-method summary is at payment-method grain. A payment total by order is at order grain. Group by `order_id` before joining to orders.
7. **Skills practised:** Reading CSVs, `groupby()`, `agg()`, `nunique()`, merge validation, and grain awareness.

<details>
<summary>Show Solution</summary>

```python
payments = pd.read_csv(data_dir / "olist_order_payments_dataset.csv")

payment_method_summary = (
    payments
    .groupby("payment_type")
    .agg(
        payment_records=("payment_sequential", "count"),
        distinct_orders=("order_id", "nunique"),
        payment_value_brl=("payment_value", "sum"),
    )
    .sort_values("payment_value_brl", ascending=False)
)

display(payment_method_summary)

payment_by_order = (
    payments
    .groupby("order_id")
    .agg(
        order_payment_total_brl=("payment_value", "sum"),
        payment_record_count=("payment_sequential", "count"),
    )
    .reset_index()
)

orders_with_payment_totals = orders_clean.merge(
    payment_by_order,
    on="order_id",
    how="left",
    validate="one_to_one",
)

display(orders_with_payment_totals.head())
```

Do not add `payment_value` to `price` and `freight_value` and describe the result as a sales total. These tables measure different things and may differ for business reasons. Use item prices for the product-sales analysis in Challenge 7.

</details>

## 6.8 Challenge 12 — Measure delivery performance

1. **Objective:** Calculate delivery duration and identify delivered orders received after their estimated delivery date.
2. **Dataset:** `orders_clean`.
3. **Relevant columns:** `order_id`, `order_status`, `order_purchase_timestamp`, `order_delivered_customer_date`, and `order_estimated_delivery_date`.
4. **Instructions:**
    1. Filter to `order_status == "delivered"`.
    2. Confirm that the actual and estimated delivery date columns are datetime values.
    3. Create `delivery_duration_days` as the time between purchase and actual delivery, measured in days.
    4. Create `delivery_delay_days` by subtracting the estimated delivery date from the actual delivery date. Compare calendar dates, not the time of day.
    5. Create `delivery_result`: `Late` if delay is greater than zero; otherwise `On time or early`.
    6. Count orders in each delivery-result group and calculate average delivery duration.
    7. Report how many delivered orders were late.
5. **Expected result:** A delivered-order DataFrame with two calculated columns and a summary of late versus on-time/early deliveries.
6. **Hints:** Use `.dt.normalize()` to set a datetime to midnight before comparing calendar dates. Use `.dt.total_seconds() / 86400` for an elapsed duration that includes partial days.
7. **Skills practised:** Filtering, datetime arithmetic, `np.where()`, calculated columns, grouping, and summary statistics.

<details>
<summary>Show Solution</summary>

```python
import numpy as np

# orders_clean dates were converted in Challenge 4.
delivered = orders_clean.loc[
    orders_clean["order_status"].eq("delivered")
].copy()

actual_date = delivered["order_delivered_customer_date"].dt.normalize()
estimated_date = delivered["order_estimated_delivery_date"].dt.normalize()

delivered["delivery_duration_days"] = (
    delivered["order_delivered_customer_date"]
    - delivered["order_purchase_timestamp"]
).dt.total_seconds() / 86400

delivered["delivery_delay_days"] = (actual_date - estimated_date).dt.days

delivered["delivery_result"] = np.where(
    delivered["delivery_delay_days"] > 0,
    "Late",
    "On time or early",
)

delivery_summary = (
    delivered
    .groupby("delivery_result")
    .agg(
        order_count=("order_id", "nunique"),
        average_delivery_duration_days=("delivery_duration_days", "mean"),
        average_delay_days=("delivery_delay_days", "mean"),
    )
)

display(delivery_summary)
print("Late delivered orders:", int(delivered["delivery_delay_days"].gt(0).sum()))
```

A positive `delivery_delay_days` means the customer received the order after the estimated calendar date. Zero or a negative value means it arrived on the estimated date or earlier. Orders that were not delivered are excluded because they do not have an actual customer-delivery date.

</details>

## 6.9 Challenge 13 — Compare review scores by delivery result

1. **Objective:** Investigate whether review scores differ between late and on-time/early delivered orders.
2. **Dataset:** `olist_order_reviews_dataset.csv` and the `delivered` DataFrame from Challenge 12.
3. **Relevant columns:** `order_id`, `review_score`, and `delivery_result`.
4. **Instructions:**
    1. Load the reviews CSV.
    2. Check the number of review rows and the number of distinct reviewed orders.
    3. Group the reviews by `order_id` and calculate the average review score and number of review rows for each order.
    4. Merge this order-level review summary with the delivered-order information from Challenge 12.
    5. Compare average review scores between `Late` and `On time or early` groups.
    6. Include the number of orders with a review in each group.
    7. Explain why this analysis shows an association, not proof that delivery timing caused a particular review score.
5. **Expected result:** A two-group summary with average review score and reviewed-order count. Orders without a review should remain missing in the joined table and should not be treated as a score of zero.
6. **Hints:** Aggregate reviews to one row per order before merging. Use `nunique()` for the reviewed-order count.
7. **Skills practised:** Reading CSVs, aggregation, left joins, missing values, grouped statistics, and cautious interpretation.

<details>
<summary>Show Solution</summary>

```python
reviews = pd.read_csv(data_dir / "olist_order_reviews_dataset.csv")

print("Review rows:", len(reviews))
print("Distinct reviewed orders:", reviews["order_id"].nunique())

review_by_order = (
    reviews
    .groupby("order_id")
    .agg(
        average_review_score=("review_score", "mean"),
        review_row_count=("review_score", "count"),
    )
    .reset_index()
)

delivery_with_reviews = delivered[
    ["order_id", "delivery_result", "delivery_delay_days"]
].merge(
    review_by_order,
    on="order_id",
    how="left",
    validate="one_to_one",
)

review_delivery_summary = (
    delivery_with_reviews
    .groupby("delivery_result")
    .agg(
        reviewed_orders=("average_review_score", "count"),
        average_review_score=("average_review_score", "mean"),
        average_delay_days=("delivery_delay_days", "mean"),
    )
)

display(review_delivery_summary)
```

The review summary is first reduced to one row per order. This avoids multiplying delivery rows when an order has multiple reviews. The `count` aggregation on `average_review_score` excludes orders without a review.

A difference between the groups is descriptive evidence only. Other factors—such as product quality, seller performance, or customer expectations—may also influence review scores.

</details>

## 6.10 Optional extension — Use `pivot_table()`

After completing the main challenges, create a table with product categories as rows and purchase years as columns. Use the sum of product `price` as the values. Use the `items_with_categories` DataFrame from Challenge 8, and merge in purchase dates from orders first. Make sure you define whether you include all order statuses or only delivered orders.

<details>
<summary>Show Solution</summary>

```python
category_items_with_dates = items_with_categories.merge(
    orders_clean[["order_id", "order_status", "order_purchase_timestamp"]],
    on="order_id",
    how="inner",
    validate="many_to_one",
)

category_items_with_dates = category_items_with_dates.loc[
    category_items_with_dates["order_status"].eq("delivered")
].copy()

category_items_with_dates["purchase_year"] = (
    category_items_with_dates["order_purchase_timestamp"].dt.year
)

category_year_pivot = pd.pivot_table(
    category_items_with_dates,
    index="category_name",
    columns="purchase_year",
    values="price",
    aggfunc="sum",
    fill_value=0,
)

display(category_year_pivot)
```

This pivot table reports product price totals by category and year for delivered orders. `fill_value=0` is appropriate here for an empty category/year combination in this summary; it is not a general rule for replacing missing source data.

</details>

---

# 7. Python Fundamentals Practice

These challenges deliberately use ordinary Python alongside Pandas. Use Python for program structure, reusable logic, and working with objects; use Pandas' vectorised methods for operations across entire DataFrame columns where appropriate.

## 7.1 Challenge 14 — Practise strings, lists, tuples, sets, and dictionaries

1. **Objective:** Use Python's built-in data structures to organise information about the dataset.
2. **Dataset:** `customers`, `orders_clean`, and their column names.
3. **Relevant columns:** `customer_state`, `order_status`, and the date columns in `orders_clean`.
4. **Instructions:**
    1. Create a list containing the three starting dataset names.
    2. Create a tuple containing the five order date column names converted in Challenge 4.
    3. Create a sorted set of distinct, non-missing state abbreviations. Clean each string using `.strip()` and `.upper()` before adding it.
    4. Create a dictionary that explains the meanings of `order_id`, `customer_id`, and `customer_unique_id`.
    5. Create a dictionary containing the count of each order status.
    6. Print the number of distinct state abbreviations and the number of order statuses.
5. **Expected result:** A list, tuple, set-derived sorted list, and two dictionaries. The customer identifier descriptions must distinguish the per-order customer record from the unique customer identity.
6. **Hints:** Sets remove duplicates. Use a dictionary comprehension or `.items()` to turn a Series into a dictionary. `str.strip()` removes leading and trailing whitespace.
7. **Skills practised:** Strings, lists, tuples, sets, dictionaries, loops, comprehensions, and type conversion.

<details>
<summary>Show Solution</summary>

```python
dataset_names = ["orders", "order_items", "customers"]

order_date_columns = (
    "order_purchase_timestamp",
    "order_approved_at",
    "order_delivered_carrier_date",
    "order_delivered_customer_date",
    "order_estimated_delivery_date",
)

state_codes = sorted(
    {
        str(state).strip().upper()
        for state in customers["customer_state"].dropna()
    }
)

identifier_meanings = {
    "order_id": "Identifies an order.",
    "customer_id": "Identifies the customer record associated with an order.",
    "customer_unique_id": "Identifies the actual customer across their orders.",
}

status_counts = orders_clean["order_status"].value_counts()
status_count_dict = {
    str(status): int(count)
    for status, count in status_counts.items()
}

print("Datasets:", dataset_names)
print("Order date columns:", order_date_columns)
print("Number of state codes:", len(state_codes))
print("State codes:", state_codes)
print("Number of order statuses:", len(status_count_dict))
print("Status counts:", status_count_dict)
print("Identifier meanings:", identifier_meanings)
```

The curly braces in `state_codes` create a set comprehension. `sorted()` turns the set into a sorted list for predictable display order. The dictionary comprehension converts Pandas values into ordinary Python values.

</details>

## 7.2 Challenge 15 — Practise conditions, `for`, `while`, and comprehensions

1. **Objective:** Use Python control flow to classify order statuses and create a small text report.
2. **Dataset:** `orders_clean`.
3. **Relevant columns:** `order_status`.
4. **Instructions:**
    1. Get the count of each status using `value_counts()`.
    2. Write a Python function `classify_status(status)` that returns `Completed` for `delivered`, `Cancelled` for `canceled`, and `Other` for every other value.
    3. Use a `for` loop to create a dictionary that maps each status to its classification.
    4. Use a list comprehension to create one report line per status, including the status name and count.
    5. Use a `while` loop to print the report lines one at a time by removing the first remaining line from a separate list.
    6. In a Markdown cell, explain why a Pandas operation is usually preferable to a Python loop when transforming millions of DataFrame rows.
5. **Expected result:** A status-to-classification dictionary and a printed report line for every status. The `while` loop should finish when no lines remain.
6. **Hints:** Use `.items()` to loop over a Series as `(index, value)` pairs. `list.pop(0)` removes and returns the first list element.
7. **Skills practised:** Functions, `if` / `elif` / `else`, `for`, `while`, list and dictionary comprehensions, and formatted strings.

<details>
<summary>Show Solution</summary>

```python
def classify_status(status):
    if status == "delivered":
        return "Completed"
    elif status == "canceled":
        return "Cancelled"
    else:
        return "Other"

status_counts = orders_clean["order_status"].value_counts()

status_classifications = {}
for status, count in status_counts.items():
    status_classifications[status] = classify_status(status)

report_lines = [
    f"{status}: {int(count)} orders ({status_classifications[status]})"
    for status, count in status_counts.items()
]

remaining_lines = report_lines.copy()
while remaining_lines:
    print(remaining_lines.pop(0))

print("\nClassifications:", status_classifications)
```

The `while` loop is included to practise Python control flow. For large data transformations, prefer Pandas methods such as `.map()`, `.where()`, `.mask()`, `.groupby()`, or vectorised comparisons rather than looping over every DataFrame row.

</details>

## 7.3 Challenge 16 — Write reusable functions and use a lambda

1. **Objective:** Turn repeated analysis logic into a function and practise a lambda function.
2. **Dataset:** `items_with_categories` from Challenge 8 and `customers`.
3. **Relevant columns:** Any valid grouping column and numeric column in `items_with_categories`; `customer_state` in customers.
4. **Instructions:**
    1. Write a function named `summarise_numeric_by_group(data, group_column, value_column)`.
    2. The function must group by `group_column` and return the count, sum, and mean of `value_column`, sorted by sum from highest to lowest.
    3. Call the function with `category_name` and `price`.
    4. Create a lambda function that removes leading/trailing whitespace and converts a state abbreviation to uppercase.
    5. Use that lambda with `.map()` on the non-missing `customer_state` values.
    6. Print the first five results.
5. **Expected result:** A reusable grouped summary and a Series of cleaned state abbreviations.
6. **Hints:** A function should return its result rather than only printing it. A lambda is a short anonymous function; it is useful for a small expression, not for complicated multi-step logic.
7. **Skills practised:** Function definitions, parameters, arguments, return values, `groupby()`, `agg()`, lambda, and `.map()`.

<details>
<summary>Show Solution</summary>

```python
def summarise_numeric_by_group(data, group_column, value_column):
    summary = (
        data
        .groupby(group_column)[value_column]
        .agg(["count", "sum", "mean"])
        .sort_values("sum", ascending=False)
    )
    return summary

category_price_summary = summarise_numeric_by_group(
    items_with_categories,
    "category_name",
    "price",
)

display(category_price_summary.head(10))

clean_state = lambda value: value.strip().upper()
cleaned_states = customers["customer_state"].dropna().map(clean_state)

print(cleaned_states.head())
```

The function receives a DataFrame and the names of two columns, so it can be reused with different group/value combinations. The lambda is intentionally simple. If the logic became longer, write a named function instead.

</details>

## 7.4 Challenge 17 — Use `pathlib`, modules, imports, and exception handling

1. **Objective:** Move CSV loading into a reusable Python module and handle a missing file with a clear error message.
2. **Dataset:** Any CSV file inside `data/raw/`.
3. **Relevant columns:** Not applicable; this challenge focuses on file handling.
4. **Instructions:**
    1. Open `src/data_loader.py` in your editor.
    2. Import `Path` and Pandas inside that file.
    3. Write a function `load_csv(filename)` that builds the path to `data/raw/filename` relative to the module's location.
    4. Use `try` / `except FileNotFoundError` to raise a clearer error that names the missing file and expected directory.
    5. Import `load_csv` in your notebook and use it to load the orders file.
    6. Test the error handling by calling it with a filename that does not exist. Confirm that the message is understandable.
5. **Expected result:** A function in `src/data_loader.py` that can load a CSV without depending on the notebook's current working directory. A missing file produces a clear `FileNotFoundError`.
6. **Hints:** `Path(__file__).resolve()` gives the path of the module file. `parents[1]` goes from `src/data_loader.py` to the project root. Use `raise ... from error` to keep the original exception context.
7. **Skills practised:** Modules, imports, functions, `pathlib`, relative paths, `try` / `except`, and raising exceptions.

<details>
<summary>Show Solution</summary>

Put this code in `src/data_loader.py`:

```python
from pathlib import Path
import pandas as pd


PROJECT_ROOT = Path(__file__).resolve().parents[1]
RAW_DATA_DIR = PROJECT_ROOT / "data" / "raw"


def load_csv(filename):
    file_path = RAW_DATA_DIR / filename

    try:
        return pd.read_csv(file_path)
    except FileNotFoundError as error:
        raise FileNotFoundError(
            f"Could not find '{filename}'. Expected it at: {file_path}"
        ) from error
```

Then, in the notebook, run:

```python
from src.data_loader import load_csv

orders_from_module = load_csv("olist_orders_dataset.csv")
print(orders_from_module.shape)
```

Test the error message:

```python
load_csv("this_file_does_not_exist.csv")
```

The final line should raise `FileNotFoundError`. That is expected for this test. Do not leave the intentional error as the last cell in a notebook you plan to publish; move it into a clearly labelled testing cell or remove it after checking.

If you edit `data_loader.py` after importing it, restart the notebook kernel and import it again, or learn about `importlib.reload()` later. Restarting is simpler while you are learning.

</details>

---

# 8. Data Visualization

Use Matplotlib for the first charts. Seaborn is optional; you can use it later when you are comfortable with Matplotlib figures and axes.

## 8.1 Chart guidelines

A chart should answer a question, not just decorate the notebook.

- Give every chart a meaningful title.
- Label both axes and include units where appropriate.
- Sort category charts so comparisons are easy.
- Avoid showing dozens of category names on one crowded chart. Start with the top ten.
- Format currency as BRL (Brazilian real), not dollars.
- State whether a sales chart includes all order statuses or only delivered orders.
- Save finished charts to `reports/figures/`.

## 8.2 Challenge 18 — Visualise monthly product sales

1. **Objective:** Create a chart showing monthly product sales for delivered orders.
2. **Dataset:** `monthly_sales` from Challenge 7.
3. **Relevant columns:** `purchase_month` index and `product_sales_brl` values.
4. **Instructions:**
    1. Create a Matplotlib figure with a readable width and height.
    2. Plot monthly product sales as a line chart or bar chart.
    3. Add a title and axis labels.
    4. Make the month labels readable.
    5. Save the chart as `reports/figures/monthly_product_sales.png`.
    6. Write one or two sentences describing a pattern you can actually see.
5. **Expected result:** A saved PNG chart with chronological months and a clearly labelled BRL value axis.
6. **Hints:** A Pandas Series has a `.plot()` method. Use `fig.tight_layout()` before saving. Convert the monthly PeriodIndex to strings if you prefer labels like `2017-01`.
7. **Skills practised:** Matplotlib, Pandas plotting, figure sizing, axis labels, file paths, and saving output.

<details>
<summary>Show Solution</summary>

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(12, 5))

monthly_sales["product_sales_brl"].plot(
    kind="line",
    marker="o",
    ax=ax,
)

ax.set_title("Monthly Product Sales — Delivered Orders")
ax.set_xlabel("Purchase month")
ax.set_ylabel("Product sales (BRL)")
ax.grid(True, alpha=0.3)

fig.tight_layout()
fig.savefig(
    Path("reports") / "figures" / "monthly_product_sales.png",
    dpi=150,
    bbox_inches="tight",
)
plt.show()
```

This chart uses product `price` only. If you want a separate freight chart, plot `monthly_sales["freight_brl"]` and give it its own title and axis label.

</details>

## 8.3 Challenge 19 — Visualise product categories and delivery performance

1. **Objective:** Create two charts that compare the leading product categories and the delivery-result groups.
2. **Dataset:** `category_summary` from Challenge 8 and `delivery_summary` from Challenge 12.
3. **Relevant columns:** `product_sales_brl`, `delivery_result`, and `order_count`.
4. **Instructions:**
    1. Select the ten categories with the highest product sales.
    2. Create a horizontal bar chart for those categories.
    3. Create a separate bar chart showing the number of delivered orders in each delivery-result group.
    4. Add a title and axis labels to both charts.
    5. Save them as `top_product_categories.png` and `delivery_performance.png` in `reports/figures/`.
    6. In Markdown, explain what each chart measures and one limitation of the analysis.
5. **Expected result:** Two separate PNG files. The category chart should show ten categories, and the delivery chart should show the available delivery-result groups.
6. **Hints:** Use `.head(10)` after sorting by sales. A horizontal chart is easier to read when category names are long. Use a separate `fig, ax = plt.subplots()` for each chart.
7. **Skills practised:** Sorting, selecting, bar charts, subplots' figure/axes interface, saving images, and writing evidence-based findings.

<details>
<summary>Show Solution</summary>

```python
import matplotlib.pyplot as plt

# Chart 1: top ten product categories
top_categories = category_summary.head(10).sort_values("product_sales_brl")

fig, ax = plt.subplots(figsize=(10, 6))
top_categories["product_sales_brl"].plot(kind="barh", ax=ax)
ax.set_title("Top 10 Product Categories by Product Sales")
ax.set_xlabel("Product sales (BRL)")
ax.set_ylabel("Product category")
fig.tight_layout()
fig.savefig(
    Path("reports") / "figures" / "top_product_categories.png",
    dpi=150,
    bbox_inches="tight",
)
plt.show()

# Chart 2: delivery performance
fig, ax = plt.subplots(figsize=(8, 5))
delivery_summary["order_count"].plot(kind="bar", ax=ax)
ax.set_title("Delivered Orders by Delivery Result")
ax.set_xlabel("Delivery result")
ax.set_ylabel("Number of delivered orders")
ax.tick_params(axis="x", rotation=0)
fig.tight_layout()
fig.savefig(
    Path("reports") / "figures" / "delivery_performance.png",
    dpi=150,
    bbox_inches="tight",
)
plt.show()
```

The category chart measures sum of item `price`, not profit or number of distinct buyers. The delivery chart includes only orders marked `delivered`; it does not classify orders that were cancelled or are still in transit.

</details>

## 8.4 Optional customer distribution chart

Use the `state_summary` DataFrame from Challenge 9 to create a horizontal bar chart of the ten states with the most delivered orders. Label the x-axis `Delivered orders` and the y-axis `Customer state`. In the chart title, specify that the metric is orders, not unique customers. You can create a second version with `distinct_customers` to compare the two measures.

---

# 9. Final Project Organization and GitHub Publication

## 9.1 Organise your notebooks

A beginner-friendly notebook should read like a report. Use Markdown cells to explain why you are running a section and what you learned from its output.

A recommended notebook order is:

| Notebook                        | Contents                                                                |
| ------------------------------- | ----------------------------------------------------------------------- |
| `01_data_exploration.ipynb`     | Load the CSV files, inspect their schema, and audit data quality        |
| `02_data_cleaning.ipynb`        | Convert dates, inspect missing values, and create analysis-ready copies |
| `03_sales_analysis.ipynb`       | Monthly sales, product categories, customers, and payment analysis      |
| `04_delivery_and_reviews.ipynb` | Delivery performance and review analysis                                |
| `05_visualizations.ipynb`       | Final charts and written findings                                       |

You may keep everything in one notebook at first. Split it into multiple notebooks only when the single notebook becomes difficult to navigate.

## 9.2 Move repeated code into `src/`

Do not move every line out of your notebook. The notebook is useful for exploration and explanation. Move code into `src/` when you have a function that you use repeatedly or want to keep separate from the analysis narrative.

Suggested responsibilities:

- `src/data_loader.py`: loading CSV files and validating expected file paths.
- `src/cleaning.py`: reusable cleaning functions, such as converting a known set of date columns.
- `src/analysis.py`: reusable calculations, such as monthly sales and repeat-customer summaries.

When you move a function into a module:

1. Keep the function name descriptive.
2. Give its parameters meaningful names.
3. Return results instead of printing them inside the function unless printing is its explicit purpose.
4. Avoid hard-coding notebook variables inside a function.
5. Import the function into the notebook and test it with the expected DataFrame.

## 9.3 Save and verify your charts

Every final chart should be saved in `reports/figures/`. Open the saved PNG file after exporting it. Check that labels are not cut off, category names are readable, and the chart still makes sense outside Jupyter.

Do not commit every experimental chart. Keep the clearest and most informative outputs.

## 9.4 Write your findings

For each major analysis, write a short Markdown section containing:

1. **Question:** What did you want to find out?
2. **Method:** Which tables, columns, filters, and calculations did you use?
3. **Result:** What did the output show? Use values from your actual run.
4. **Interpretation:** What might the result mean for the business?
5. **Limitation:** What does the dataset not tell you, or what should a reader be careful about?

Do not copy example numbers from another project. Run the analysis on your downloaded dataset and report the numbers you actually obtain.

## 9.5 Prepare the final GitHub README

This learning README can become the final project README after you complete the work. Add a concise project summary near the top and include:

- Project overview and goals.
- Dataset source and licence attribution.
- Tools and package requirements.
- Setup and execution instructions.
- The questions you investigated.
- A few key charts embedded with relative paths, for example:

```markdown
![Monthly product sales](reports/figures/monthly_product_sales.png)
```

- Findings supported by your analysis.
- Data and methodology limitations.
- Instructions for downloading the dataset, since the raw files are not included in the repository.

Keep the detailed learning challenges and hidden solutions only if you want the repository to remain an educational walkthrough. For a job-portfolio presentation, you may prefer a shorter front-facing README and keep detailed learning notes in the notebooks.

## 9.6 Make meaningful Git commits

Commit after a meaningful unit of work rather than waiting until the entire project is complete.

Examples:

```bash
git status
git add notebooks/01_data_exploration.ipynb
git commit -m "Explore Olist order and customer data"
```

```bash
git add src/ reports/figures/
git commit -m "Add reusable analysis functions and charts"
```

```bash
git push
```

Before every commit, inspect `git status` and make sure you are not about to commit the raw CSV files or `.venv/`.

## 9.7 Final completion checklist

- [ ] Project environment can be recreated from `requirements.txt`.
- [ ] The notebook runs from top to bottom after the dataset is downloaded.
- [ ] All source CSVs remain unchanged in `data/raw/`.
- [ ] Date columns used in calculations have datetime dtypes.
- [ ] Missing values have been investigated rather than blindly filled.
- [ ] Joins use the correct keys and have appropriate validation.
- [ ] Order-level metrics are not inflated by joining multiple one-to-many tables.
- [ ] Customer-level metrics use `customer_unique_id`.
- [ ] Product sales and freight are labelled separately.
- [ ] Charts are saved and readable.
- [ ] Findings use actual values from your run.
- [ ] Limitations and metric definitions are documented.
- [ ] Raw datasets and the virtual environment are excluded from Git.
- [ ] The repository has been pushed to GitHub.

---

# 10. Recommended Working Routine

Use a 60-minute session as a starting point:

| Time       | Activity                                                                        |
| ---------- | ------------------------------------------------------------------------------- |
| 10 minutes | Recall one Python or Pandas concept without checking notes                      |
| 40 minutes | Attempt one project challenge or make progress on the analysis                  |
| 10 minutes | Review errors, check the solution if necessary, and write down what you learned |

For every challenge:

1. Read the objective and expected result carefully.
2. Try to solve it without opening the solution.
3. Read the relevant Pandas or Python documentation when you get stuck.
4. Open the solution only after making a genuine attempt.
5. Compare the approach, not just the final output.
6. Close the solution and rewrite the code from memory.
7. Add a short note about the mistake or concept you learned.

Do not rush through all the challenges in one sitting. It is more useful to understand why a merge or aggregation is correct than to finish a long checklist quickly.

---

# 11. Dataset Notes, Definitions, and References

## 11.1 Important metric definitions used in this project

| Metric                         | Definition in this project                                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| Delivered order                | An order whose `order_status` is exactly `delivered`                                                         |
| Product sales                  | Sum of `price` from order-item rows included by the stated filter                                            |
| Freight                        | Sum of `freight_value` from order-item rows included by the stated filter                                    |
| Item plus freight              | Sum of `price + freight_value` for item lines; not profit                                                    |
| Item-line count                | Number of order-item rows; the source table has no separate quantity column                                  |
| Distinct customer              | Unique `customer_unique_id`                                                                                  |
| Repeat customer                | A `customer_unique_id` with more than one delivered `order_id` in Challenge 10                               |
| Late delivered order           | A delivered order whose actual customer-delivery calendar date is after its estimated delivery calendar date |
| Average review score per order | Mean of all available `review_score` rows for that `order_id`                                                |

These are project definitions, not universal accounting definitions. Keep them consistent when comparing results.

## 11.2 Dataset quality and interpretation cautions

- The customer table has one row per order-associated customer record. It is not a one-row-per-real-person table; use `customer_unique_id` to identify repeat customers.
- The order-items table has multiple rows per order. Aggregate it to order level before combining it with another one-to-many table when calculating order-level totals.
- The payments table can contain multiple payment records per order. Aggregate by `order_id` before adding payment totals to an order-level table.
- The reviews table may contain multiple review records for an order. Aggregate by `order_id` before joining review metrics to delivery or order data.
- The geolocation table can contain many coordinate rows for the same ZIP prefix. Aggregate it by ZIP prefix before joining it to customer or seller location data.
- Product category translations may not exist for every category. Preserve the original category name as a fallback.
- Two product column names are misspelled in the original data: `product_name_lenght` and `product_description_lenght`.
- Missing delivery timestamps are expected for orders that have not been delivered. Do not calculate delivery duration for those orders.
- The Kaggle dataset is historical. Do not describe its findings as current e-commerce market conditions.

## 11.3 Dataset licence and attribution

The Kaggle dataset page lists the licence as **CC BY-NC-SA 4.0** (Attribution-NonCommercial-ShareAlike 4.0 International). Review the licence terms before redistributing any dataset content or using it for commercial purposes. This project should link to the Kaggle source rather than upload the raw CSV files to GitHub.

Suggested attribution:

> Olist. (2018). _Brazilian E-Commerce Public Dataset by Olist_ [Data set]. Kaggle. https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

## 11.4 References

- [Olist Brazilian E-Commerce Public Dataset — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- [Project Jupyter — Installing Jupyter](https://jupyter.org/install)
- [Python Downloads](https://www.python.org/downloads/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/)
- [Seaborn Documentation](https://seaborn.pydata.org/)
- [Git Documentation](https://git-scm.com/doc)
- [Community-maintained Olist data dictionary and relationship notes](https://github.com/NFP-05/End-to-End-Olist-E-Commerce-Platform/blob/main/docs/data_dictionary.md) — useful as a schema cross-check; the CSV files downloaded from Kaggle remain the source of truth.

---

**Start here:** Complete Step 2, create the folders in Step 3, download the dataset in Step 4, and then attempt Challenge 1. Do not move to analysis until you can load and inspect the three starting DataFrames yourself.
