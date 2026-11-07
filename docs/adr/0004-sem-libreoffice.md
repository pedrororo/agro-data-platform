# ADR 0004 — Ler planilhas com pandas/xlrd, sem LibreOffice

**Status:** aceita (2026-11-07)

## Contexto
O `big_data` convertia os `.xls` do Cepea com o LibreOffice porque o `xlrd` os rejeita como "corrompidos"
(`CompDocError: Workbook corruption`). LibreOffice deixa a imagem pesada e frágil.

## Decisão
Ler direto com pandas: `.xls` via `xlrd` com `ignore_workbook_corruption=True`; `.xlsx` via `openpyxl`.
Testado em 2026-11-07 com as 8 planilhas do `big_data`: mesmos valores do CSV gerado pelo LibreOffice.

## Consequências
- + Sem dependência de sistema; imagem menor; leitura testável.
- − O modo tolerante pode aceitar um arquivo realmente danificado: por isso a validação de contrato (cabeçalho, datas, números) é obrigatória depois da leitura.
