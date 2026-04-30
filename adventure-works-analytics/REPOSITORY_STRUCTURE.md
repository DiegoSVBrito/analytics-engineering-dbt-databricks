# Adventure Works Analytics - Repository Structure

## � Directory Organization

```
adventure-works-analytics/
├── .github/                              # GitHub configuration
│   ├── workflows/                        # GitHub Actions CI/CD
│   │   ├── dbt-ci.yml                   # DBT continuous integration
│   │   ├── dbt-docs.yml                 # Documentation deployment
│   │   └── release.yml                  # Release automation
│   ├── ISSUE_TEMPLATE/                  # Issue templates
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── data_quality_issue.md
│   ├── pull_request_template.md         # PR template
│   ├── BRANCH_STRATEGY.md              # Branching guidelines
│   └── CONTRIBUTING.md                 # Contribution guidelines
│
├── dbt_project/                         # Main dbt project
│   ├── analyses/                        # Analytical queries
│   │   ├── customer_cohort_analysis.sql
│   │   ├── product_performance_trends.sql
│   │   └── territory_growth_analysis.sql
│   │
│   ├── dbt_packages/                    # dbt packages (gitignored)
│   │
│   ├── logs/                           # dbt logs (gitignored)
│   │
│   ├── macros/                         # Custom dbt macros
│   │   ├── generate_schema_name.sql
│   │   ├── test_helpers.sql
│   │   └── business_metrics.sql
│   │
│   ├── models/                         # dbt models
│   │   ├── staging/                    # Raw data cleaning
│   │   │   ├── api_sales/
│   │   │   ├── products/
│   │   │   ├── sales/
│   │   │   └── sources/
│   │   │       └── sources.yml
│   │   │
│   │   ├── intermediate/               # Business logic
│   │   │   ├── int_sales__enriched.sql
│   │   │   ├── int_products__hierarchy.sql
│   │   │   └── intermediate.yml
│   │   │
│   │   └── marts/                      # Business-ready models
│   │       ├── dimensions/             # Dimension tables
│   │       │   ├── dim_customer.sql
│   │       │   ├── dim_product.sql
│   │       │   └── dim_date.sql
│   │       │
│   │       ├── sales/                  # Sales mart
│   │       │   ├── fact_sales_transactions.sql
│   │       │   └── fact_sales_monthly_agg.sql
│   │       │
│   │       ├── dim_customers_enhanced.sql      # Analytical dimensions
│   │       ├── dim_products_performance.sql
│   │       ├── dim_territories_performance.sql
│   │       ├── dim_channels_performance.sql
│   │       ├── dim_product_associations.sql
│   │       └── marts.yml
│   │
│   ├── seeds/                          # CSV reference data
│   │   ├── territory_mappings.csv
│   │   └── product_categories.csv
│   │
│   ├── snapshots/                      # SCD Type 2 tracking
│   │   ├── customers_snapshot.sql
│   │   └── products_snapshot.sql
│   │
│   ├── tests/                          # Custom data tests
│   │   ├── assert_positive_clv.sql
│   │   ├── assert_valid_lifecycle_stages.sql
│   │   ├── assert_valid_lift_values.sql
│   │   └── assert_revenue_consistency.sql
│   │
│   ├── target/                         # dbt artifacts (gitignored)
│   │
│   ├── dbt_project.yml                 # dbt project configuration
│   ├── packages.yml                    # dbt package dependencies
│   └── CLAUDE.md                       # Claude Code instructions
│
├── orchestration/                       # Airflow orchestration
│   ├── dags/                           # Airflow DAGs
│   │   ├── adventure_works_etl.py
│   │   └── data_quality_monitoring.py
│   │
│   ├── config/                         # Configuration files
│   │   ├── profiles.yml
│   │   └── airflow.cfg
│   │
│   ├── docker-compose.yml              # Docker setup
│   ├── Dockerfile                      # Container definition
│   ├── requirements.txt               # Python dependencies
│   └── .env.example                   # Environment variables template
│
├── docs/                               # Project documentation
│   ├── architecture/                  # Architecture documentation
│   │   ├── data_model_diagram.md
│   │   ├── pipeline_architecture.md
│   │   └── security_model.md
│   │
│   ├── business/                       # Business documentation
│   │   ├── kpis_and_metrics.md
│   │   ├── data_dictionary.md
│   │   └── use_cases.md
│   │
│   ├── technical/                      # Technical documentation
│   │   ├── setup_guide.md
│   │   ├── deployment_guide.md
│   │   ├── troubleshooting.md
│   │   └── api_documentation.md
│   │
│   └── images/                        # Documentation images
│       ├── architecture_diagram.png
│       └── data_lineage.png
│
├── scripts/                            # Utility scripts
│   ├── setup/                         # Setup scripts
│   │   ├── install_dependencies.sh
│   │   ├── setup_databricks.sh
│   │   └── configure_profiles.sh
│   │
│   ├── deployment/                     # Deployment scripts
│   │   ├── deploy_dev.sh
│   │   ├── deploy_prod.sh
│   │   └── run_tests.sh
│   │
│   └── maintenance/                    # Maintenance scripts
│       ├── backup_data.sh
│       ├── cleanup_logs.sh
│       └── health_check.py
│
├── environments/                       # Environment configurations
│   ├── dev/                           # Development environment
│   │   ├── profiles.yml
│   │   └── env_vars.yml
│   │
│   ├── staging/                       # Staging environment
│   │   ├── profiles.yml
│   │   └── env_vars.yml
│   │
│   └── prod/                          # Production environment
│       ├── profiles.yml
│       └── env_vars.yml
│
├── tests/                             # Project-level tests
│   ├── integration/                   # Integration tests
│   │   ├── test_data_pipeline.py
│   │   └── test_api_endpoints.py
│   │
│   ├── unit/                         # Unit tests
│   │   ├── test_transformations.py
│   │   └── test_business_logic.py
│   │
│   └── performance/                   # Performance tests
│       ├── test_query_performance.py
│       └── benchmark_pipeline.py
│
├── .gitignore                         # Git ignore rules
├── .pre-commit-config.yaml           # Pre-commit hooks
├── README.md                          # Project overview
├── CHANGELOG.md                       # Version history
├── LICENSE                           # Project license
└── requirements.txt                   # Python dependencies (root level)
```

## � File Descriptions

### Core dbt Files
- **`dbt_project.yml`**: Project configuration, model paths, and materialization settings
- **`packages.yml`**: External dbt package dependencies
- **`CLAUDE.md`**: Instructions for Claude Code AI assistant

### Data Models
- **`staging/`**: Raw data cleaning and standardization (views)
- **`intermediate/`**: Business logic and complex joins (views)
- **`marts/`**: Final business-ready models (tables)

### Orchestration
- **`orchestration/`**: Airflow DAGs and Docker configuration
- **`dags/`**: ETL pipeline definitions and scheduling

### Documentation
- **`docs/`**: Comprehensive project documentation
- **`README.md`**: Quick start guide and project overview

### CI/CD
- **`.github/workflows/`**: Automated testing and deployment
- **`scripts/`**: Utility scripts for setup and maintenance

## � Configuration Files

### Environment-Specific
Each environment (dev/staging/prod) has its own:
- Database connection profiles
- Environment variables
- Deployment configurations

### Git Configuration
- **`.gitignore`**: Excludes target/, logs/, .env files
- **`.pre-commit-config.yaml`**: Code quality checks
- **GitHub templates**: Standardized PR and issue formats

## � Asset Organization

### By Layer (Medallion Architecture)
- **Bronze**: `staging/` - Raw data ingestion
- **Silver**: `intermediate/` - Cleaned and joined data
- **Gold**: `marts/` - Business-ready analytics

### By Domain
- **Sales**: Customer, orders, revenue analytics
- **Products**: Catalog, performance, lifecycle
- **Territories**: Geographic performance and ROI

### By Purpose
- **Facts**: Transaction and aggregated data
- **Dimensions**: Descriptive attributes and hierarchies
- **Analytics**: Advanced calculations and insights
