# 🐼 Pandas Practice

> **Goal:** Load, clean, explore and summarise real-world tabular data with Pandas: the first step of every ML project.

Part of my [20-week AI/ML Engineer journey](https://github.com/<your-username>/ml-journey) · Builds on [numpy-practice](https://github.com/<your-username>/numpy-practice)

---

## Why Pandas?
NumPy is great for numbers in grids, but real data has **column names, mixed types, missing values and dates**. Pandas adds labelled tables (**DataFrames**) on top of NumPy, so I can clean and analyse data the way I'd use a spreadsheet or SQL, but with code that's repeatable and fast.

## 📈 Progress

Following [Kaggle Learn: Pandas](https://www.kaggle.com/learn/pandas) (6 lessons).

| # | Lesson | Notebook | Status |
|---|---|---|---|
| 1 | Creating, Reading and Writing | [`01_creating_reading_writing.ipynb`](01_creating_reading_writing.ipynb) | ✅ |
| 2 | Indexing, Selecting and Assigning | [`02_indexing_selecting_assigning.ipynb`](02_indexing_selecting_assigning.ipynb) | ✅ |
| 3 | Summary Functions and Maps | `03_summary_functions_maps.ipynb` | ⬜ |
| 4 | Grouping and Sorting | `04_grouping_sorting.ipynb` | ⬜ |
| 5 | Data Types and Missing Values | `05_dtypes_missing_values.ipynb` | ⬜ |
| 6 | Renaming and Combining | `06_renaming_combining.ipynb` | ⬜ |

Status key: ⬜ Not started · 🟡 In progress · ✅ Done

---

## 1️⃣ Creating, Reading and Writing

| Task | Code |
|---|---|
| DataFrame from a dictionary (keys = columns) | `pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})` |
| Custom row labels | `pd.DataFrame({...}, index=['Product A', 'Product B'])` |
| Series from a list | `pd.Series([1, 2, 3, 4, 5])` |
| Series with labels and a name | `pd.Series([87, 89], index=['P1', 'P2'], name='Product sales')` |
| Read a CSV | `pd.read_csv("data/file.csv")` |
| Use first column as index | `pd.read_csv("data/file.csv", index_col=0)` |
| Size of the table | `df.shape` → `(rows, columns)` |
| First rows | `df.head()` |
| Write a CSV | `df.to_csv("out.csv", index=False)` |

**In my own words:** a **DataFrame** is a whole table; a **Series** is one column of it. A dictionary becomes a DataFrame (each key is a column), a list becomes a Series. CSV means *Comma-Separated Values*: a table saved as plain text.

## 2️⃣ Indexing, Selecting and Assigning

| Task | Code |
|---|---|
| One column | `data['company_name']` (or `data.company_name`) |
| One value | `data.loc[2, 'date_of_manufacture']` |
| Row by position | `data.iloc[4]` |
| Column by position | `data.iloc[:, 0]` |
| Rows & columns by position (end excluded) | `data.iloc[0:3, 0:2]` |
| Named columns | `data.loc[:, ['date_of_manufacture', 'company_name']]` |
| Rows by label (end **included**) | `data.loc[0:3, 'company_name']` |
| True/False per row | `data['product_number'] == 4` |
| Filter rows | `data.loc[data['company_rating'] >= 8]` |
| AND / OR | `data.loc[(cond1) & (cond2)]` · `data.loc[(cond1) \| (cond2)]` |
| Match a list | `data.loc[data['company_name'].isin(['Amazon Star', 'Data Delta'])]` |
| Set a whole column | `data['company_name'] = 'google'` |
| Set one value | `data.loc[0, 'company_name'] = 'Nova Labs'` |

### `iloc` vs `loc`: the key difference

| | `iloc` | `loc` |
|---|---|---|
| Selects by | **position** (0, 1, 2…) | **label** (index labels, column names) |
| Order | `[row, column]` | `[row, column]` |
| End of a range | **excluded** (`0:3` → 0, 1, 2) | **included** (`0:3` → 0, 1, 2, 3) |

## ⚠️ Lessons learned

- **It's `iloc[row, column]`, rows first.** My first notes said column first, which was wrong.
- **Prefer `data['col']` over `data.col`.** Brackets work for every column name, including ones with spaces or names like `count` that clash with pandas methods.
- **Use `.loc[row, col]` to change one value.** Chained indexing like `data['col'][2] = x` doesn't reliably change the original table.
- **Assigning one value overwrites the whole column.** `data['company_name'] = 'google'` changed all 16 rows. Use `.copy()` first if I want to keep the original.
- **Use `&` and `|`, not `and` / `or`, and put each condition in brackets.**
- **Define the data once, at the top.** A cell that relies on a column created in an old, deleted cell breaks on *Restart & Run All*.

## 🗂️ Datasets
Lessons 1–2 use small sample tables created inside the notebooks, so they run with no downloads.

| Dataset | Source | Used in |
|---|---|---|
| Wine Reviews | [Kaggle: Wine Reviews](https://www.kaggle.com/datasets/zynicide/wine-reviews) | Kaggle exercises (Lessons 1–6) |

Large data files are not committed (see `.gitignore`). Download them into `data/`.

## ▶️ How to run

```bash
git clone https://github.com/<your-username>/pandas-practice.git
cd pandas-practice
python -m venv .venv
# Windows: .venv\Scripts\activate   |   Mac/Linux: source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

## 📚 Resources
- [Kaggle Learn: Pandas](https://www.kaggle.com/learn/pandas)
- Wes McKinney: [Python for Data Analysis, 3rd ed.](https://wesmckinney.com/book/) (Ch. 5)
- [Pandas User Guide: Indexing and selecting data](https://pandas.pydata.org/docs/user_guide/indexing.html)
