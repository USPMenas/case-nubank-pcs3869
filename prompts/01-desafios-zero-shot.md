# Prompt 01 — Desafios identificados — zero shot

| Campo | Valor |
| --- | --- |
| Atividade do cronograma | 2.3 — Listar os desafios identificados |
| Técnica | Zero shot (sem exemplos) |
| Modelo usado (gerador) | Claude Opus 5.5, no claude.ai |
| Data da execução | 09/11/2026 |
| Operado por | Claude, a pedido do grupo (papel: Engenheiro de prompts — Ian) |
| Saída usada em | `item-a-proposta/proposta.md`, seção 2 |

## Prompt

**Objetivo:** Listar os desafios que a proposta de consultoria deve resolver na integração de informações entre NuPay e cartão de crédito.

**Domínio:** Sistemas de informação aplicados a crédito ao consumidor e meios de pagamento.

**Contexto:** O Nubank oferece o NuPay, um meio de pagamento para compras online em estabelecimentos parceiros, com três modalidades: débito (saldo em conta), crédito (limite do cartão) e limite adicional (temporário, exclusivo do NuPay, parcelado em até 24x com juros e sujeito a análise). As compras no crédito e no limite adicional entram na fatura do cartão. A hipótese do grupo é que dados e regras de NuPay e cartão não têm uma visão integrada, o que dificulta ajustar taxas e risco de forma coordenada. Soluções como parcela mínima e post purchase financing (financiamento após a compra) são afetadas.

**Persona:** Você é um consultor sênior de sistemas de informação, com experiência em bancos digitais e no modelo de Laudon e Laudon (administração, organização e tecnologia).

**Atividades:**
1. Leia o contexto e o diagnóstico de entrada.
2. Identifique os desafios de informação, de regras e de governança.
3. Classifique cada desafio numa dimensão do modelo de Laudon.
4. Descreva o impacto de cada desafio em uma frase.
5. Indique quais soluções (parcela mínima, post purchase financing ou ambas) cada desafio afeta.

**Definições:**
- Desafio: uma dificuldade que um sistema de informação pode reduzir, não uma falha comprovada do Nubank.
- Alinhamento: decisões coerentes com o contexto de cada produto; não pressupõe taxas idênticas.
- Use só informação pública; não invente números, taxas nem volumes.

**Formato de saída:** Tabela em Markdown com as colunas ID (D1, D2…), Desafio, Dimensão (Administração, Organização ou Tecnologia), Impacto e Soluções afetadas. Entre 4 e 6 linhas. Sem texto antes ou depois da tabela.

**Descrição de entrada:** Resumo do diagnóstico do grupo, em tópicos, colado abaixo.

---

**Entrada:**

- O limite adicional e as regras de parcelamento do NuPay impactam a fatura do cartão de crédito.
- Não existe alinhamento perfeito entre NuPay e cartão, então fica difícil ajustar taxas e risco.
- Dados e regras dos dois produtos não têm visão integrada (hipótese).
- Consequência esperada: mais esforço para comparar condições e coordenar ofertas.
- Proposta de valor: um sistema de informação com dados e regras integrados (histórico de compras e crédito; taxas, prazos e elegibilidade; regras versionadas e rastreáveis).

## Saída obtida

| ID | Desafio | Dimensão | Impacto | Soluções afetadas |
| --- | --- | --- | --- | --- |
| D1 | Dados do cliente divididos entre NuPay e cartão (limite regular, limite adicional, parcelas e fatura) | Tecnologia | Nenhum produto enxerga sozinho a exposição total do cliente | Ambas |
| D2 | Regras de taxas, prazos e elegibilidade definidas por produto, sem uma base comum | Administração | Condições oferecidas ao mesmo cliente podem divergir sem motivo claro | Ambas |
| D3 | Ajuste de taxas e risco feito sem considerar o efeito no outro produto | Administração | Uma mudança em um produto altera o risco da fatura sem ser avaliada em conjunto | Ambas |
| D4 | Comparação de condições trabalhosa, com bases e critérios diferentes | Organização | Mais esforço dos times para comparar e coordenar ofertas | Parcela mínima; post purchase financing |
| D5 | Mudanças de regra sem versionamento e rastreio comuns | Tecnologia | Difícil saber qual regra valia, quando mudou e por quê | Ambas |

## Avaliação do grupo (a preencher)

- [ ] Os desafios refletem o diagnóstico da apresentação?
- [ ] Algum desafio afirma como fato o que é hipótese?
- [ ] Algum desafio depende de dado interno do Nubank?
- Decisão: aceito / aceito com ajustes / refazer — por quem, em que data.

Nota para a auditoria (S3): como o gerador foi o Claude, o LLM auditor deve ser outro (ChatGPT ou Gemini).
