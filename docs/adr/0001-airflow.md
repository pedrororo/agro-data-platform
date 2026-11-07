# ADR 0001 — Airflow 3 como orquestrador

**Status:** aceita (2026-11-07)

## Contexto
Precisamos agendar coletas, repetir falhas, fazer backfill do histórico e ver o que rodou e quando.

## Opções
- **Airflow 3** — padrão de mercado; o mais pedido em vagas de engenharia de dados. Mais pesado localmente (~4 GB de RAM).
- **Dagster** — orientado a assets, partições e backfill de primeira classe, mais leve. Menos presente em vagas.
- **Cron + scripts** — simples, mas sem retries, histórico, backfill nem visibilidade.

## Decisão
Airflow 3, com LocalExecutor no docker compose.

## Consequências
- + Habilidade diretamente reconhecida em vagas; conceitos (DAG, data lógica, backfill, retries) valem para qualquer orquestrador.
- − Exige disciplina para manter as DAGs só como orquestração (lógica no pacote `agro/`, testável sem Airflow).
- − Consumo de memória local maior.
