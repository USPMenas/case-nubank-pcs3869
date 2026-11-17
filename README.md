# case-nubank-pcs3869

Trabalho final de PCS3869: proposta de consultoria para integrar as informações do NuPay e do cartão de crédito do Nubank.

**Grupo:** Lucas Carvalho · Ian Magalhães · Rafael Tamasi

## Estrutura

| Pasta / arquivo | O que é |
|---|---|
| [NuPay e cartão de crédito.pdf](NuPay%20e%20cart%C3%A3o%20de%20cr%C3%A9dito.pdf) | Apresentação do case. |
| [NuPay e cartão de crédito - Entrega 3.pdf](NuPay%20e%20cart%C3%A3o%20de%20cr%C3%A9dito%20-%20Entrega%203.pdf) | Enunciado da entrega 3. |
| [item-a-proposta/](item-a-proposta/) | Item A: proposta v1, cronograma, planilha de custos, anexo de alinhamento de taxas e BPMN/PNG do processo proposto. |
| [item-c-processo/](item-c-processo/) | Item C: processo usado pelo grupo, atores e papéis (v1), com BPMN/PNG. |
| [prompts/](prompts/) | Prompts: 01 desafios (zero shot), 02 serviços (few shot), 03 custos (chain of thought), 04 auditor (persona). |
| [auditoria/](auditoria/) | Auditoria cruzada entre LLMs (rodada 1: pacote para o auditor). |
| [planejamento/cronograma-e-papeis.xlsx](planejamento/cronograma-e-papeis.xlsx) | Cronograma (uma entrega por semana até 01/12/2026), papéis e atores × papéis. |

## Diário

| Data | Autor | Item | O que foi feito | Arquivos | LLM | Commit |
| --- | --- | --- | --- | --- | --- | --- |
| 2026-11-17 | Lucas | Planejamento | Status do cronograma: S2 100%, S3 em andamento (auditoria e achados) | planejamento/cronograma-e-papeis.xlsx | — | 4328eae |
| 2026-11-17 | Rafael | Auditoria, Prompts | Prompt de auditor (Persona de Auditor) e pacote pronto para colar | prompts/04-auditor.md; auditoria/rodada-1/pacote-para-colar.md | — | df59a72 |
| 2026-11-17 | Lucas, Ian | A | Proposta v1 (4 páginas): alinhamento de taxas, cronograma e investimento | item-a-proposta/proposta.md | Claude Opus 5.5 | 0944ebb |
| 2026-11-17 | Ian | A | Anexo técnico: como funciona o alinhamento de taxas (fórmula, regras R1 a R6, exemplo) | item-a-proposta/alinhamento-de-taxas.md | Claude Opus 5.5 | 8fdec8d |
| 2026-11-17 | Rafael | A, Prompts | Planilha de custos com prompt chain of thought: 2.042 h, total R$ 522.824,50 | prompts/03-custos-cot.md; item-a-proposta/planilha-custos.xlsx | Claude Opus 5.5 | 3d74bc0 |
| 2026-11-17 | Rafael | A | Cronograma da consultoria: 16 semanas, 4 marcos, caminho crítico | item-a-proposta/cronograma.md | Claude Opus 5.5 | 5ee41cd |
| 2026-11-17 | — | Case | Enunciado da entrega 3 | NuPay e cartão de crédito - Entrega 3.pdf | — | 05c7936 |
| 2026-11-17 | Lucas | B | Fechamento da semana 2 e tag `entrega-s2` | README.md | — | 32ab98c |
| 2026-11-17 | Lucas | Planejamento | Status do cronograma atualizado: S1 100%, S2 80% (falta só esta tag) | planejamento/cronograma-e-papeis.xlsx | — | 29e2d41 |
| 2026-11-17 | Ian | A | Rascunho v0 da proposta, com contexto, desafios, serviços e solução | item-a-proposta/proposta.md; solucao-processo.bpmn; solucao-processo.png | — | 2ccf17e |
| 2026-11-17 | Ian | A, Prompts | Serviços S1 a S6 desenhados com prompt few shot (2 exemplos de outro setor) | prompts/02-servicos-few-shot.md | Claude Opus 5.5 | c6af074 |
| 2026-11-17 | Ian | A, Prompts | Desafios D1 a D5 levantados com prompt zero shot | prompts/01-desafios-zero-shot.md | Claude Opus 5.5 | 0c9e087 |
| 2026-11-17 | Lucas | C | Texto do Item C v1 (3 páginas): fluxo, etapas, atores, papéis e regras | item-c-processo/item-c.md; processo.bpmn; processo.png | Claude Opus 5.5 | fae3208 |
| 2026-11-03 | — | Planejamento | Cronograma e papéis, BPMN da solução e índice no README | cronograma-e-papeis.xlsx; solucao-processo.bpmn | — | 2e51b03 |
| 2026-11-03 | — | — | Apresentação NuPay e cartão de crédito | NuPay e cartão de crédito.pdf | — | 9dd81c0 |
