# ADR 0003 — Cepea por depósito manual, sem scraping

**Status:** aceita (2026-11-07)

## Contexto
O site do Cepea responde 403 a acessos automatizados (Cloudflare) e o robots.txt bloqueia robôs. Contornar isso viola as regras do site.

## Opções
- **Depósito manual** — a pessoa baixa no navegador e sobe no bucket `inbox`; o pipeline detecta e valida.
- **Acesso licenciado** (ex.: via empresa) — melhor no longo prazo, mas depende de contrato.
- **Scraping contornando o bloqueio** — descartado.

## Decisão
Depósito manual no `inbox`. Se surgir acesso licenciado, ele vira só outra forma de chegar ao mesmo `inbox`.

## Consequências
- + Padrão real e comum ("o parceiro manda um arquivo"); o pipeline não muda se a origem mudar.
- + Mantém o desafio real: validar arquivos de terceiros que podem mudar de formato.
- − Atualização depende de alguém subir o arquivo; precisamos de um alerta de "dado atrasado" (Fase 3).
- Os dados do Cepea não vão para o git (licença e tamanho); só pequenas fixtures de teste.
