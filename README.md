# Analytics Engineering - dbt + Databricks

Pipeline end-to-end de analytics implementando arquitetura medalhao (Bronze/Silver/Gold) com dbt no Databricks, orquestracao Airflow e CI/CD automatizado.

## Arquitetura

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

Orquestracao: Apache Airflow
CI/CD: GitHub Actions
Transformacao: dbt-core + dbt-databricks
Storage: Databricks (Delta Lake)
```

## Dimensiones Analiticas

| Modelo | Descricao |
|--------|-----------|
| `dim_customers_enhanced` | Customer Lifetime Value (CLV) com segmentacao VIP/Premium/Regular/Basic |
| `dim_products_performance` | Ciclo de vida de produtos (Crescimento/Maturidade/Declinio/Descontinuado) |
| `dim_territories_performance` | ROI territorial com rankings de eficiencia |
| `dim_channels_performance` | Performance de canais (Online vs Reseller) |
| `dim_product_associations` | Market basket analysis com metricas lift/confidence/support |

## Tecnologias

- **dbt**: Transformacao e testes de dados
- **Databricks**: Compute e storage (Delta Lake)
- **Apache Airflow**: Orquestracao de pipelines
- **GitHub Actions**: CI/CD automatizado
- **Docker**: Containerizacao para deploy
- **SQL**: Linguagem principal de transformacao

## Como Executar

```bash
# Instalar dependencias
pip install dbt-databricks
dbt deps

# Executar modelos
dbt run

# Executar 45+ testes automatizados
dbt test

# Gerar documentacao
dbt docs generate && dbt docs serve
```

## Decisoes Tecnicas

**Por que dbt + Databricks?** O dbt permite versionar transformacoes SQL com testes e documentacao automatica. O Databricks fornece compute elástico com Delta Lake para armazenamento transacional. A combinacao elimina a necessidade de ETL manual e garante rastreabilidade completa da linhagem dos dados.

**Por que arquitetura medalhao?** Separa claramente as camadas de responsabilidade. Bronze recebe dados brutos sem transformacao (garantindo reprocessabilidade). Silver aplica regras de negocio. Gold serve modelos prontos para consumo por ferramentas de BI. Cada camada pode ser reprocessada independentemente.

**Por que GitHub Actions?** Cada push dispara testes automaticos que validam os modelos dbt. Se um modelo quebra, o PR e bloqueado. Isso garante que somente transformacoes validas chegam ao ambiente de producao.

## Estrutura do Repositorio

```
adventure-works-analytics/
  models/
    staging/         # Camada Bronze
    intermediate/    # Camada Silver
    marts/           # Camada Gold
  tests/             # Testes customizados dbt
  analyses/          # Queries analíticas ad-hoc
  orchestration/     # DAGs Airflow
  dbt_project.yml    # Configuracao do projeto
```

## Resultados de Negocio

- **Customer Analytics**: Segmentacao por CLV para estrategias de retencao
- **Product Analytics**: Identificacao de produtos em declinio para otimizacao de catalogo
- **Territory Analytics**: Rankings de ROI por territorio
- **Channel Analytics**: Comparacao Online vs Reseller
- **Market Basket**: Associacao de produtos para cross-selling

---

**Autor:** Diego Brito
