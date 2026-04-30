# Analytics Engineering - dbt + Databricks

End-to-end analytics pipeline implementing medallion architecture (Bronze/Silver/Gold) with dbt on Databricks, Airflow orchestration, and automated CI/CD.

## Architecture

```
                    +------------------+
                    |   Data Sources   |
                    |  (AdventureWorks |
                    |    SQL Server)   |
                    +--------+---------+
                             |
                    +--------v---------+
                    |     BRONZE       |
                    |  Staging Models  |
                    | (raw ingestion)  |
                    +--------+---------+
                             |
                    +--------v---------+
                    |      SILVER      |
                    |  Intermediate    |
                    | (business logic) |
                    +--------+---------+
                             |
                    +--------v---------+
                    |       GOLD       |
                    |   Marts / DIM    |
                    | (analytics-ready)|
                    +--------+---------+
                             |
                    +--------v---------+
                    |   Dashboards /   |
                    |   Reports / BI   |
                    +------------------+

Orchestration: Apache Airflow
CI/CD: GitHub Actions
Transformation: dbt-core + dbt-databricks
Storage: Databricks (Delta Lake)
```

## Analytical Dimensions

| Model | Description |
|-------|-------------|
| `dim_customers_enhanced` | Customer Lifetime Value (CLV) with VIP/Premium/Regular/Basic segmentation |
| `dim_products_performance` | Product lifecycle analysis (Growth/Maturity/Decline/Discontinued) |
| `dim_territories_performance` | Territory ROI with efficiency rankings |
| `dim_channels_performance` | Channel performance (Online vs Reseller) |
| `dim_product_associations` | Market basket analysis with lift/confidence/support metrics |

## Technologies

- **dbt**: Data transformation and testing
- **Databricks**: Compute and storage (Delta Lake)
- **Apache Airflow**: Pipeline orchestration
- **GitHub Actions**: Automated CI/CD
- **Docker**: Containerized deployment
- **SQL**: Primary transformation language

## Usage

```bash
pip install dbt-databricks
dbt deps
dbt run
dbt test
dbt docs generate && dbt docs serve
```

## Technical Decisions

**Why dbt + Databricks?** dbt allows versioning SQL transformations with tests and automatic documentation. Databricks provides elastic compute with Delta Lake for transactional storage. The combination eliminates manual ETL and ensures full data lineage traceability.

**Why medallion architecture?** Clearly separates layers of responsibility. Bronze ingests raw data without transformation (enabling reprocessing). Silver applies business rules. Gold serves analytics-ready models to BI tools. Each layer can be reprocessed independently.

**Why GitHub Actions?** Every push triggers automatic tests validating dbt models. If a model breaks, the PR is blocked. This ensures only valid transformations reach production.

## Repository Structure

```
adventure-works-analytics/
  models/
    staging/         # Bronze layer
    intermediate/    # Silver layer
    marts/           # Gold layer
  tests/             # Custom dbt tests
  analyses/          # Ad-hoc analytical queries
  orchestration/     # Airflow DAGs
  dbt_project.yml    # Project configuration
```

## Business Outcomes

- **Customer Analytics**: CLV-based segmentation for retention strategies
- **Product Analytics**: Declining product identification for catalog optimization
- **Territory Analytics**: ROI rankings by territory
- **Channel Analytics**: Online vs Reseller performance comparison
- **Market Basket**: Product association for cross-selling

---

Author: Diego Brito
