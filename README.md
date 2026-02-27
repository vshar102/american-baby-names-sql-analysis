# American Baby Names Trends (1920–2020)

This project analyzes 101 years of U.S. baby name data from the United States Social Security Administration. Using PostgreSQL, the notebook explores long-term naming trends, historical popularity rankings, and the distinction between enduring “classic” names and short-lived trends.

The analysis focuses on identifying patterns in name longevity, frequency dominance, and century-spanning popularity.

---

## 📊 Dataset

The dataset includes first names given to **more than 5,000 babies in a given year**.

**Primary Table: `baby_names`**

| Column       | Type    | Description                                   |
| ------------ | ------- | --------------------------------------------- |
| `year`       | INT     | Year of record                                |
| `first_name` | VARCHAR | Baby’s first name                             |
| `sex`        | VARCHAR | Sex of babies with that name                  |
| `num`        | INT     | Number of babies given that name in that year |

---

## 🔍 Project Analysis

The notebook answers three core analytical questions using SQL:

### 1️⃣ Classification of Top Names — *Classic vs. Trendy*

**Objective:**
Identify the overall top five names (alphabetically) and classify them based on historical longevity.

**Approach:**

* Aggregated total occurrences per name
* Used `COUNT(year)` to measure name longevity
* Applied a `CASE` statement:

  * > 50 years of presence → **Classic**
  * ≤ 50 years → **Trendy**
* Limited output to the top five names

**Key Concept:** Conditional aggregation with classification logic.

---

### 2️⃣ Ranking Top Male Names (1920–2020)

**Objective:**
Determine the top 20 male names across the century and assign ranks based on total frequency.

**Approach:**

* Filtered dataset with `sex = 'M'`
* Calculated total occurrences using `SUM(num)`
* Applied window function:

  ```sql
  RANK() OVER (ORDER BY SUM(num) DESC)
  ```
* Grouped by name and limited to 20 results

**Key Concept:** Window functions for ranking historical dominance.

---

### 3️⃣ Enduring Female Names (1920 vs. 2020)

**Objective:**
Identify female names that appeared in both 1920 and 2020 — measuring true century-spanning relevance.

**Approach:**

* Performed a self-join on `baby_names`
* Filtered for:

  * `sex = 'F'`
  * One record in 1920
  * Matching record in 2020
* Calculated combined total occurrences for those two years

**Key Concept:** Self-joins for longitudinal comparison.

---

## 🛠 Technologies Used

* **SQL (PostgreSQL dialect)**
* **Jupyter Notebook (DataCamp Workspaces)**

---

## 🎯 Project Highlights

* Applied aggregation, conditional logic, window functions, and self-joins
* Analyzed over a century of structured historical data
* Demonstrated practical SQL techniques for trend analysis and longitudinal data comparison
