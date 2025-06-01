# DSRS Knowledge-Base Prototype

**What’s inside**  
Prototype KB (`dsrs_kb_source.csv`), a NetworkX graph converted to an
interactive PyVis HTML (`dsrs_graph.html`), and a fully-reproducible notebook
(`DSRS_KB_Prototype.ipynb`).

**How to run**

1. Open `DSRS_KB_Prototype.ipynb` and run *Runtime ▸ Run all*  
2. When execution finishes, double-click `dsrs_graph.html` in the file browser
   to explore the graph.

**Key files**

| File | Purpose |
| ---  | --- |
| `dsrs_kb_source.csv` | Source rows for the knowledge-base (23 rows) |
| `dsrs_graph.html`    | Interactive graph (23 nodes / 20 edges) |
| `DSRS_KB_Prototype.ipynb` | Notebook that builds the CSV, graph and demo queries |

**Sources**  
All KB rows cite:

* `DSRS Strategy.pdf`
* Public pages on **dsrs.illinois.edu**
* LinkedIn post permalinks (last 6 months)

## Maintenance & Growth Strategy

### 1 . Keeping the KB current
| Task | Owner | Frequency | Tooling |
|------|-------|-----------|---------|
| **Automated scrape** of DSRS website and LinkedIn (new posts, new datasets) → append to `dsrs_kb_source.csv` | Infrastructure | nightly cron on DSRS server | Python + GitHub Actions |
| **CSV diff review**: check duplicates / stale rows flagged by `last_updated` > 90 days | Sub-unit leads | monthly | notebook validator |
| **Manual additions** (new projects, workshop decks) | Services & Data Hub staff | ad-hoc | KB template form (Google Form → Zapier → CSV row) |

### 2 . Accuracy controls
* All rows include a `source` URL/PDF; rows without a source fail the CI check.  
* `last_updated` timestamp is overwritten on every save so ageing rows are obvious.  
* Graph build step refuses to run if duplicate `id` values are detected.

### 3 . Integration with day-to-day workflows
* **New project kickoff** → PM completes a 5-line KB form; CI merges it automatically.  
* **LinkedIn post** → Zapier webhook auto-creates a `news` row with `post_date`.  
* **Dataset on-boarding** in Data Hub playbook now ends with “add dataset to KB” step.  
* Monthly DSRS all-hands starts with the KB growth chart so gaps are visible.

### 4 . Road-map (next 6 months)
1. Migrate CSV to a lightweight Postgres table exposed via REST.  
2. Build a Neo4j mirror for advanced graph queries.  
3. Embed a Streamlit KB search app on the DSRS intranet.  
4. Add unit tests to guarantee schema consistency before every merge.


