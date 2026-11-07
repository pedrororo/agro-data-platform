# ADR 0002 — MinIO + Parquet como armazenamento

**Status:** aceita (2026-11-07)

## Contexto
Precisamos guardar originais imutáveis e uma camada padronizada, num modelo que depois vá para a nuvem sem reescrever tudo.

## Opções
- **MinIO (S3 local) + Parquet** — mesmo modelo de S3 / Azure Blob / GCS; Parquet é colunar, comprimido e lido por DuckDB, Spark, dbt.
- **Só Postgres** — mais simples, mas não ensina o modelo de data lake e mistura arquivos originais com tabelas.

## Decisão
MinIO com buckets `inbox`, `landing`, `quarentena`, `bronze`; bronze em Parquet particionado por série e ano; DuckDB para consultas.

## Consequências
- + Migrar para a nuvem é trocar endpoint e credenciais.
- + Separação clara entre original (imutável) e dado padronizado (reconstruível).
- − Sem transações entre arquivos: a idempotência vem de reescrever partições inteiras e caminhos determinísticos.
