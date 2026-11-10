# case-nubank-pcs3869

Trabalho final de PCS3869: proposta de consultoria para integrar as informações do NuPay e do cartão de crédito do Nubank.

**Grupo:** Lucas Carvalho · Ian Magalhães · Rafael Tamasi

## Estrutura

| Pasta / arquivo | O que é |
|---|---|
| [NuPay e cartão de crédito.pdf](NuPay%20e%20cart%C3%A3o%20de%20cr%C3%A9dito.pdf) | Apresentação do case. |
| [item-a-proposta/](item-a-proposta/) | Item A: proposta de consultoria (rascunho v0) e BPMN/PNG do processo proposto. |
| [item-c-processo/](item-c-processo/) | Item C: processo usado pelo grupo, atores e papéis (v1), com BPMN/PNG. |
| [prompts/](prompts/) | Prompts usados com LLM: 01 desafios (zero shot) e 02 serviços (few shot). |
| [planejamento/cronograma-e-papeis.xlsx](planejamento/cronograma-e-papeis.xlsx) | Cronograma (uma entrega por semana até 01/12/2026), papéis e atores × papéis. |

## Diário

| Data | Autor | Item | O que foi feito | Arquivos | LLM | Commit |
| --- | --- | --- | --- | --- | --- | --- |
| 2026-11-17 | Lucas | B | Fechamento da semana 2 e tag `entrega-s2` | README.md | — | este commit |
| 2026-11-17 | Lucas | Planejamento | Status do cronograma atualizado: S1 100%, S2 80% (falta só esta tag) | planejamento/cronograma-e-papeis.xlsx | — | 29e2d41 |
| 2026-11-17 | Ian | A | Rascunho v0 da proposta, com contexto, desafios, serviços e solução | item-a-proposta/proposta.md; solucao-processo.bpmn; solucao-processo.png | — | 2ccf17e |
| 2026-11-17 | Ian | A, Prompts | Serviços S1 a S6 desenhados com prompt few shot (2 exemplos de outro setor) | prompts/02-servicos-few-shot.md | Claude Opus 5.5 | c6af074 |
| 2026-11-17 | Ian | A, Prompts | Desafios D1 a D5 levantados com prompt zero shot | prompts/01-desafios-zero-shot.md | Claude Opus 5.5 | 0c9e087 |
| 2026-11-17 | Lucas | C | Texto do Item C v1 (3 páginas): fluxo, etapas, atores, papéis e regras | item-c-processo/item-c.md; processo.bpmn; processo.png | Claude Opus 5.5 | fae3208 |
| 2026-11-03 | — | Planejamento | Cronograma e papéis, BPMN da solução e índice no README | cronograma-e-papeis.xlsx; solucao-processo.bpmn | — | 2e51b03 |
| 2026-11-03 | — | — | Apresentação NuPay e cartão de crédito | NuPay e cartão de crédito.pdf | — | 9dd81c0 |
