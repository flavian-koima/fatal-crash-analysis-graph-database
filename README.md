
#  Fatal Crash Analysis Using Graph Databases

### *A Data Warehousing + Neo4j Project by Flavian Jerotich*

This project transforms a large flat CSV dataset of Australian fatal crashes into a **graph database** to uncover complex patterns, improve analytical flexibility, and enable powerful real-world insights into road safety.

It demonstrates:

* Data modelling
* ETL pipeline development (Python + Pandas)
* Graph database schema design
* Cypher querying
* Graph Data Science (Community Detection)
* Interpretive analytics

---

## **1. Project Overview**

This project was completed as part of *CITS5504 – Data Warehousing*.
The goal was to convert a traditional dataset into a **property graph model** that supports rich, multidimensional analysis using **Neo4j**.

The dataset comes from the
**Australian Road Deaths Database (Bureau of Infrastructure, Transport and Regional Economics)**.

A graph database was chosen because road crashes involve interconnected attributes such as:

* location
* road type
* road user
* time/day
* vehicle involvement
* remoteness

These relationships are better expressed as a **graph**, not a flat table.

---

##  **2. Graph Schema Design**

The graph was designed using **Arrows App**.

### **Nodes**

* `Crash`
* `RoadUser`
* `State`
* `LGA`
* `SA4`
* `Remoteness`
* `RoadType`

### **Relationships**

| Relationship         | From → To          | Meaning                                     |
| -------------------- | ------------------ | ------------------------------------------- |
| `INVOLVED`           | Crash → RoadUser   | Person involved in the crash                |
| `OCCURRED_IN_STATE`  | Crash → State      | Crash location (state)                      |
| `OCCURRED_IN`        | Crash → LGA        | Local Government Area                       |
| `LOCATED_IN_SA4`     | Crash → SA4        | Statistical Area Level 4                    |
| `IN_REMOTENESS_AREA` | Crash → Remoteness | ABS remoteness region                       |
| `HAPPENED_ON`        | Crash → RoadType   | Road classification (highway/arterial/etc.) |

This normalized graph reduces redundancy and improves query performance.

---

##  **3. ETL Process (Python)**

Python was used to:

* Load original CSV (10,490 rows × 25 columns)
* Clean, validate, and deduplicate
* Create node CSVs
* Create relationship CSVs
* Export all files into Neo4j import folder

Key steps included:

```python
df = pd.read_csv("Project2_Dataset_Corrected.csv")
unique_states = df["State"].drop_duplicates()
```

All generated CSVs are included in the `/data` folder.

---

## 🧠 **4. Cypher Queries & Insights**

Several analytical queries were implemented, including:

### 🔸 Crashes involving articulated trucks in WA (2020–2024)

### 🔸 Minimum and maximum ages of motorcycle riders

### 🔸 Weekend vs weekday trends for young drivers

### 🔸 Friday multi-fatality crashes with both genders

### 🔸 Top SA4 regions for peak-hour crashes

### 🔸 Pedestrian crashes involving trucks/buses at extreme speeds

Each query included:

* Output table
* Interpretation
* Screenshots

See `/queries` folder.

---

##  **5. Graph Data Science: Community Detection**

Using **Neo4j GDS**, a Louvain Modularity analysis was performed to detect structural crash clusters.

```cypher
CALL gds.louvain.stream('lgaCrashGraph')
YIELD nodeId, communityId
```

Results:

* **509 unique communities**
* **Modularity ≈ 0.996** (very high)
* Identified strong clusters of crashes within specific LGAs

These findings support targeted interventions in regional areas.

---



## **6. Skills Demonstrated**

This project showcases:

### ✔ Data Warehousing & Modelling

### ✔ ETL Engineering (Python, Pandas)

### ✔ NoSQL / Graph Database Design

### ✔ Cypher Query Language

### ✔ Data Visualisation & Insight Writing

### ✔ Graph Data Science (Louvain Clustering)

### ✔ Real-world safety analytics

Perfect for roles in:

* Data Analyst
* BI Analyst
* Junior Data Scientist
* Data Engineer (entry level)

---

## **8. Contact**

**Author:** *Flavian Jerotich*
Master of Data Science



