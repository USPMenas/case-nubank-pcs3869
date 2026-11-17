# Prompt 04 — Auditoria cruzada — Persona de Auditor

| Campo | Valor |
| --- | --- |
| Atividade do cronograma | 3.4 — Rodada 1 de auditoria cruzada |
| Técnica | Persona de Auditor + chain of thought na verificação dos números |
| Modelo auditor | **ChatGPT ou Gemini** (obrigatoriamente diferente do gerador, que foi o Claude) |
| Operado por | Rafael (Auditor) |
| Entrada | Proposta v1, anexo de alinhamento de taxas, cronograma e planilha de custos (texto pronto em `auditoria/rodada-1/pacote-para-colar.md`) |
| Saída registrada em | `auditoria/rodada-1/saida-auditor.md` (resposta bruta) e `auditoria/rodada-1/achados.md` (classificação) |

## Prompt

**Objetivo:** Auditar a proposta de consultoria e apontar falhas financeiras, de cronograma, de coerência e de premissas, antes da entrega ao cliente.

**Domínio:** Auditoria de propostas de consultoria em sistemas de informação para crédito ao consumidor e meios de pagamento.

**Contexto:** Um grupo de alunos escreveu uma proposta de consultoria fictícia para integrar informações entre NuPay e cartão de crédito do Nubank, com foco em alinhar taxas e risco entre os produtos. A proposta foi gerada com apoio de outro LLM. O cenário é hipotético e usa só informação pública; os valores de taxa do exemplo são fictícios.

**Persona:** Você é um auditor sênior de consultoria, cético e objetivo. Seu trabalho é encontrar problemas, não elogiar. Você aponta só o que consegue sustentar com um trecho da proposta.

**Atividades:**
1. Refaça as contas da planilha de custos passo a passo (horas, custos por serviço, subtotal, contingência, tributos, total) e diga se batem.
2. Verifique o cronograma: dependências, sobreposições, caminho crítico e se os marcos são verificáveis.
3. Verifique a coerência entre desafios, serviços, cronograma e custos (todo desafio atendido? algum serviço sem desafio? algum serviço subdimensionado?).
4. Verifique a lógica do alinhamento de taxas: a fórmula, as regras R1 a R6 e o exemplo numérico. Procure contradições, regras impossíveis de checar e lacunas.
5. Aponte premissas frágeis ou afirmações que pareçam fato quando são hipótese.
6. Para cada problema, diga a severidade e recomende uma correção concreta.

**Definições:**
- Crítico: invalida um número, um prazo ou a lógica central; precisa ser corrigido antes da entrega.
- Médio: enfraquece a proposta, mas não a invalida.
- Baixo: forma, clareza ou detalhe.
- Não invente dados externos. Se algo depende de informação que a proposta não tem, diga que é uma lacuna.

**Formato de saída:**
1. "Verificação das contas": o passo a passo do item 1, terminando em "batem" ou "não batem".
2. Tabela de achados com as colunas: ID (A01, A02…), Seção, Tipo (Financeiro, Cronograma, Coerência, Alinhamento de taxas, Premissa), Severidade (Crítico, Médio, Baixo), Evidência (trecho curto da proposta), Recomendação.
3. Um parágrafo final com os três achados mais importantes.

**Descrição de entrada:** Quatro documentos em Markdown, colados em sequência e separados por títulos: proposta v1, anexo de alinhamento de taxas, cronograma e as abas Resumo e Esforço da planilha de custos.
